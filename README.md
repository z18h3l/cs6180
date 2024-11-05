java c
CO 372: Portfolio Optimization Models 
Fall 2024 
Problem Set 4
Handed out: 2024-10-23.Due:  Fri, 2024-11-01, 4pm EDT, on Crowdmark.  Papers must be handed in on-line using the labeled dropbox on Crowdmark. The Crowdmark link will be sent out on the same day this is posted.  Each question is handed in as a separate upload.  You can either prepare your solutions electronically using, e.g., LaTeX, or else you can hand-write them and submit a scan.  In the latter case, please take care that the scan is of good quality with a white background.Your papers may be handed in up to 24 hours late, in which case there is a 10% late penalty. Please use the late-paper dropbox on Crowdmark if you are handing in a late paper. 	You may hand in some questions on time and others late.  In this case, use the on-time dropbox for the on-time questions and the late dropbox for the late questions.  However, you may not split the parts of a question (i.e., (a), (b), etc.)  between the two dropboxes.Collaboration policy. This problem set is a solo effort.  Students are allowed to discuss question with each other in general terms including helping each other on Piazza. However, no student should share an entire solution to a question, nor should any student hand in work that entirely represents someone else’s effort.
1.  We are given a Pr3′ instance with all the usual assumptions, that is, the version of Pr3 in which there are n − 1 risky securities and a single risk-free security available whose return is rf . Assume there is a single wealth constraint.
A formula was given in lecture for a value tm  > 0 (the “market point”) such that the portfolio [tmH −1 (r(¯) − rf e);0] is optimal for Pr3′ for the choice t := tm  in Pr3′ .
(a) Turn this around: given an arbitrary tm  > 0, positive definite matrix H ∈ Sn−1, and vector r(¯) ∈ Rn−1, find a formula rf  so that the optimizer for Pr3′  is [tmH −1 (r(¯)−rf e);0].Explain why the formula is valid (and in particular, does not involve division by 0) because of all the assumptions made.
(b) Does the formula extend to tm  = 0?  Explain.
(c) Does the rf  that emerges from the formula in (a) satisfy the inequality α0  > rf , which was assumed in lecture? Explain.
2.  Consider Pr3′ .  As usual, assume t ≥ 0 and H is positive definite.  Suppose (contrary to the usual assumption) that α0  < rf , where α0 is the return of the min-risk portfolio that uses only risky investments.
(a) The formulas from lecture show that the optimal portfolio has the form.  where x(ˆ) = tx′  and xn   = 1 − teT x′ , where x′  ∈ Rn−1  depends on H , r(¯), and rf , and
that this optimal portfolio never short-sells the risk-free security. Explain.
(b) Show that there must be at least one risky security i ∈ {1, . . . , n − 1} such that every optimal portfolio (for all t ≥ 0) invests an amount ≤ 0 in that security.
3.  Pr1′ , which was presented in lecture, may be reformulated as: minxTHx/2 subject to Ax = b, r(¯)Tx − q = rp , q ≥ 0.  In other words, a slack variable q has been introduced, and a sign constraint is imposed on the slack variable. Call this formulation Pr1′ S (S
for “slack”). Assume H ∈ Sn , A ∈ Rp ×n , b ∈ Rp , r(¯) ∈ Rn.
(a) Write down the KKT conditions for Pr1′ S.  Note that there are no general-form. inequality constraints in Pr1′ S, but there is a sign constraint. Label the four parts.Caution: The gradient equation of Pr1′ S involves vectors of length n + 1 rather than n because there are n+1 problem variables [x;q].  There are p+1 equality constraints in these n + 1 variables. Using block matrix notation, rewrite the equality constraints in terms of a (p+1)×(n+1) matrix before attempting to write the gradient equation. Similarly, the objective function should be rewritten as [corrected on 2024-10-27]:
in order for the LHS of the gradient equation to come out correctly.
(b) Argue that from any solution for the KKT conditions of Pr1′ (which were presented in lecture), a solution to the KKT conditions of Pr1′ S may be obtained.
(c) Argue that from any solution for 代 写CO 372: Portfolio Optimization Models Fall 2024 Problem Set 4Matlab
代做程序编程语言the KKT conditions of Pr1′ S, a solution to the KKT conditions of Pr1′ may be obtained.
4.  (a) Write down the KKT conditions for the capital asset pricing model that appears on Slide 5 of M22.  Clearly identify four parts.  Note that the gradient equation involves the matrix H+ , not H alone.(b) Make all the assumptions in M20–M22.  Show that if t > tm , where tm  is defined in Slide 4 of M21,then xn  = 0 in the optimizer to the problem of Slide 5 of M22. Suggested approach for a proof by contradiction:  If xn   >  0, then the KKT complementarity condition requires a certain multiplier to be 0.  If this multiplier is 0, then the KKT conditions of this problem reduce to the KKT conditions for the problem of Slide 5 in M20. But for t > tm , that optimizer to that problem is not feasible for the problem at hand.
5. The function fmincon in Matlab can solve general constrained minimization problems (although it is not always the best method). Consider the problem of maximizing the Sharpe ratio given H , r(¯), and rf , assuming a single budget constraint. This can be set up as an optimization problem.Write the following functions in Matlab. The first takes these three values H , r(¯), and rf , and then invokes fmincon to maximize the Sharpe ratio. There is one constraint, namely, the budget constraint. It returns the optimal portfolio. Here is the header:
function  [x,errflag]  = maximize_sharpe(H,  rbar,  rf)
%  Return  the  optimizer  of  the  Sharpe  ratio  given  data  H,  rbar,  and %  rf .    If  fmincon  fails,  the  errflag=true,  else  errflag=false .Here are some tips on fmincon.   Type  doc  fmincon  for  a  description of its input and output arguments. You need to retrieve the first three output arguments so that you can examine  exitflag in order to determine how to set  errflag.   This  is  a minimization routine, so to maximize a function, give its negative as the objective. The first argument is a function handle.  A function handle in Matlab has the form. @(x)(), where x is the argument of the function (not a variable in the surrounding code that you write).   For  example,  if  you  wanted  to minimize the function x2  − ax, where a is a coefficient, you would say
a  =  .  .  . ;
my_fhandle  =  @(x)(x^2  -  a*x);
[optx,fval,exitflag]  =  fmincon(my_fhandle,  . . .)
For maximizing the  Sharpe  ratio,  there  are  no  inequality  constraints  and  a  single equality constraint. Use the vector (1/n,..., 1/n) as the starting guess.Write a second function that plots the efficient frontier by repeatedly maximizing the Sharpe ratio.  It should take a vector of rf ’s from the user.  For each rf , it invokes maximize_sharpe. If maximize_sharpe returns an error, then no point is plotted. In the plot statement, use the linestyle. ’-*g’, which displays a green asterisk for each point plotted and connects the asterisks with a green line. Here is the header:
function plot_efficient_frontier_sh(H,  rbar,  vector_rf)
%  Invoke maximize_sharpe  for  each  entry  of  vector_rf  (same  H  and  rbar)
%  each  time .    For  each  computed  solution  x,  work  out  the  risk
%  and  expected  return .    Plot  the  risk  and  expected  return  for
%  all  solutions  as  a  green  curve .    If  maximize_sharpe  indicates %  an  error,  then no point  is plotted .Next, download ps4_data. mat from the website to obtain H and r(¯) .  Call your function from PS3 to computerp,min, that is, the return of themin-risk portfolio of risky stocks. I got 1.0298 from my calculation.
Next, call plot_efficient_frontier_sh(H,  rbar,  vector_rf) using for argument vector_rf: linspace(.9,1.02,30), that is, 30 equally spaced points from 0.9 to 1.02.
Try again with 30 equally spaced points from 0.9 to 1.05; a strange plot will emerge.Hand in: listings of both functions, the requested plots (1.02 case and 1.05 case), and a trace of how you computed rp,min. Then write 1–2 sentences to answer the following question: Why did the code work poorly for the 1.05 case?

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
