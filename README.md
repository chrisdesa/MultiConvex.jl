# MultiConvex

[![Build Status](https://travis-ci.org/chrisdesa/MultiConvex.jl.svg?branch=master)](https://travis-ci.org/chrisdesa/MultiConvex.jl)

#############################
# Example 1
#############################

@mcvx begin
  x = var()
  minimize((x - 1)^2)
end

# result:
#   x = 1.0

#############################
# Example 2
#############################

u = randn(100)

@mcvx begin
  x = var(100);
  minimize(sum((x*x' - u*u').^2))
  init_randn()
  solver_newton(1000)
end

# result
#   x = u

#############################
# function/type reference
#############################

# abstract MCExpr
#   type of expressions
#   supports operations:
#     show
#     +, -, *

# function mcvx_begin()
#    initializes an mcvx model

# function var()
# function var(dim1::Int64)
# function var(dim1::Int64, dim2::Int64)
#   produces a new variable in an mcvx scope, or an array of such variables

# function minimize(expr::MCExpr)
# function maximize(expr::MCExpr)
#   provides an objective for the problem

# function solver_coorddesc(numiters::Int64, step_size::Float64)
#   selects the first-order coordinate descent solver
#   (default)

# function solver_newton(numiters::Int64)
# function solver_newton(numiters::Int64, alpha::Float64)
#   selects the second-order (newton's method) coordinate descent solver

# function init_zero()
#   specifies to initialize the problem variable to zero

# function init_randn()
#   specifies to initialize the problem variable with randn

# function mcvx_end()
#   finishes the mcvx model and solves the problem

# function resolve(expr::MCExpr)
#   after mcvx_end called, returns the value of a variable in the solution

# macro var(symbol, dims...)
#   wrapper around the var(...) function that gives the variable a name in
#   the displayed version of the expression

# macro mcvx(block)
#   automatically wraps the block in appropriate mcvx_begin() and mcvx_end()
#   statements, and automatically generates resolve(...) calls at the end
#   to places the variables back into local scope

