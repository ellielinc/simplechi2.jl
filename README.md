###### Chi Squared Minimization and Plotting

## Plot data points with errorbars

```
using PyPlot
x_data = [0.0, 2, 4, 6, 8, 10]
y_data = [3.0, 5, 8, 6, 7, 9]
sigma_data = 0.5*ones(6);
uppererror = sigma_data'/2;
lowererror = sigma_data'/2;
errs = [lowererror;uppererror]
x_data = map(Float64,x_data)
fig = figure("best_fit_chisq",figsize=(10,10))
pe = errorbar(x_data,y_data,yerr=errs,fmt="o", color="Green")
axis("tight")
ax = axes()
title("Points of Best Fit")
xlabel("x Data")
ylabel("y Data")
grid("on")
gcf()
```
## Define function of alpha
Basic chi-squared equation

`f= alpha->sum((y_data-(alpha[1]*x_data+alpha[2])./sigma_data).^2)`

## Find chisq and alpha values
Here, usung the Nelder-Mead algorithm in NLopt.
```
using NLopt;

chisq=(alpha,g)->sum((((alpha[1]*x_data+alpha[2]) - y_data)./sigma_data).^2)

opt = Opt(:LN_NELDERMEAD, 2);
min_objective!(opt, chisq);
(minf,minx,ret) = optimize(opt, [1.234, 5.678]);
println("got $minf at $minx (returned $ret)")
```
## Plot function with NLopt alpha values.
Plug in returned `$minx` values for alpha.

```alpha=[0.485714,3.90476]
y_model= (alpha[1]*x_data+alpha[2])
scatter(x_data, y_model, color="Red")```

