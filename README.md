# MLTP_Programming_Assignment

Description:

Given an EUF formula with multiple arity functions, check Satisfiability using Shostak’s Algorithm.
[Alvin George and Prathamesh Patil, MLTP-2023 Course, 2023 March]

Implement Python3.9
Z3 has a python interface.
You can call Z3 as Propositional Logic solver (SAT Solver).
But have to implement the EUF solving by yourselves using Shostak’s algorithm.
Input given as a z3py expression.  (You don’t have to read from text file).
Output is just saying if the given EUF formula is SAT or UNSAT.

Following are 2 examples of possible input z3 expressions.
S = DeclareSort('S')
f = Function('f', S, S)
x = Const('x', S)
formula1 = And(f(f(x)) == x, f(f(f(x))) == x)
formula2 = And(f(f(x)) == x, f(f(f(x))) == x, f(x) != x)

It is possible to just use solve(formula1) to get a solution (or “no solutions”, in the case of unsatisfiable formulae such as formula2), but obviously that goes against the point of the project; you must implement the Shostak algorithm yourself.
Formulae/terms in z3 are trees, so one can use various functions to help traverse through the operators and terms present in it. See following:

print("num args: ", formula1.num_args())
print("children: ", formula1.children())
print("1st child:", formula1.arg(0))
print("2nd child:", formula1.arg(1))
print("operator: ", formula1.decl())
print("op name:  ", formula1.decl().name())

In order to get the arity of a function, you can use f.arity(). Declaration of n-ary function is done as follows:
f = Function('f', S1, S2, S3, …, Sn, R)
Where Si is the sort of the ith input term of f, while R is the sort of the output term.

----
(Part 1) Shostak’s:
Given a conjunction of EUF equalities, return SAT or UNSAT.
(Part 2) DPLL(T):
1.	Convert the given formula into a corresponding proportional formula B.
2.	Call z3 to check if B is satisfiable.
3.	Use the solution to determine the satisfiability of the equality and disequality classes using the Shostak’s algorithm.

Look at DPLL(T) algorithm from KS book. Here is a brief summary:
DPLL(T): Convert the given E-formula φ to a PL formula e(φ) by
replacing equalities with new propositional variables. Check for satisfiability using a PL solver. If UNSAT, return UNSAT. If SAT, see if
the assignment corresponds to a satisfiable equality assignment (for
example using the induced equality graph). If it does, return SAT;
else add a clause to e(φ) corresponding to the conflicting equality
assignments, and repeat.
But using z3 as the DPLL SAT solver.


Helpful Links:
https://ericpony.github.io/z3py-tutorial/guide-examples.htm
https://theory.stanford.edu/~nikolaj/programmingz3.html

----
Code your implementation in a file named:  euf_shostak.py.
In that file Implement the following two function
Part1:
def euf_solver_shostak(euf_formula_list)
which returns either z3.sat, z3.unsat or z3.unknown 

Part2: 
def euf_dpllt_solver(general_euf_formula)
which returns either z3.sat, z3.unsat or z3.unknown 


You can have other functions / subroutines etc within the file.
1.	Print the PL formula that you construct initially and also whenever you modify it.
2.	Print the clause that is added
We will later provide a utility functions to print the formula.
Note:
Use python 3.9.15
We will evaluate it by running on python-3.9.15


![image](https://user-images.githubusercontent.com/88618946/230263034-e0a680c0-69cc-4758-acbb-9e1bc2da79d2.png)
