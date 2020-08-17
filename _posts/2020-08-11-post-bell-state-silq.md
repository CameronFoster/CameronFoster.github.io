---
title: Bell State in Silq
categories:
  - Blog
tags:
  - jupyter notebook
  - Silq
  - Bell State
  - Python
  - quantum programming
author: Alberto Maldonado Romo
---

# About Silq

Silq is a new high-level programming language for quantum computing with a strong static type system, developed at ETH Zürich.

# Installation
The official link https://silq.ethz.ch/install has the comands to install in vscode or in linux/Mac Os distributions.

# Introduction to Silq


For this first example we must take into account the following properties of the silq language:


### B type variables are Boolean variables.

```python
x := false:B; // variable boolean x with the value in False

// x, means variable name
// :=, means  assignment 
// false, means value in false;
// :B, indicates the type of false value
```

### Apply pre-defined functions


```python
x := H(x); // the Hadamard gate is applied to the boolean variable x and assigned to the same variable x

// x, means variable name
//H(booleam argument) // function that apply the Hadamard function on a boolean variable
```

### Generate a function

```python
def classicalExample(x:𝔹,f:𝔹->𝔹){ // generate a examle function that has a boolean variable x 
                                    //and function f that  Boolean mapping to another Boolean
  return f(x);              // return the function f
}
```

To know more about the documentation  check the following link : https://silq.ethz.ch/documentation



# Bell State

The simplest example for quantum computation is to generate a Bell state from the controlled-not gate to or Cnot with a previous superposition of the qubit and control with the Hadamard gate.

![bell_state.png](/assets/quantum_programs/bell_state/silq/Images/bell_state.png)

# Program

The silq code to perform the previously mentioned state of bell is described.

## Generate cnot function

To generate the denied controlled gate it is necessary to indicate two boolean variables: x,y where x represents the control qubit and if it is true it denies the variable y.



```python
// B means the boolean type 
// const mens constant value in this case in the boolean variable x

def cnot(const x:B,y:B):B{ //generate the function Cnot gate
  if x{  // if x is true  apply the sentence inside the {} 
    y := X(y);  // apply X gate in the boolean variable x
  }
  return y; // return the only 
}
```

## Define main function

We initialize the boolean variables x,y in false or zero state, to the variable x we apply the Hadamard gate, followed by the cnot function where x is the control qubit over the qubit y. Finally, we measure and return the values of the qubits (obtaining their classic values from the two qubits used in the program).

```python
def main(){ // main function

  x := false:B;    // A boolean (B type) variable x is initialized in false or zero state (|0>)
  y := false:B;    // A boolean (B type) variable x is initialized in false or zero state (|0>)
  x := H(x);       // Applying Hadamard to the boolean variable x
  y := cnot(x,y);  // It called the function cnot(x,y)
  return  measure(x,y);  // return the measure by the x and y variables or qubits.
}

```

### Expect output

```python
(1,1)
(0,0)
```

A Python file was generated in order to plot the results obtained from the code previously made in silq

```python
import silq as sq

sq.init_variables(n=50,filename="bell_state.sql")
sq.plot_histogram()

```

![png](/assets/quantum_programs/bell_state/silq/Bell_state_silq_files/Bell_state_silq/Bell_state_silq_8_0.png){: .center-image }

The previous silq code is in the file called bell_state.sql in the github repo

And if you want to use the python part to plot the result histogram is the file called silq.py
