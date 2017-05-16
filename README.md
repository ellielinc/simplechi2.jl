# Chi Square Minimization and Best Fit Plotting

#Using Julia to compute and graph best fit plots to compare Model predictions and Data results.
#Packages used are PyPlot and NLopt.

#Graph the Data points

using PyPlot
x = [0, 2, 4, 6, 8, 10]
y = [3, 5, 8, 6, 7, 9]

x = map(Float64,x)

fig = figure("pyplot_scatterplot",figsize=(10,10))
ax = axes()
scatter(x,y)


fig = figure("pyplot_errorbar",figsize=(10,10)) 
p = plot_date(x,y,linestyle="-",marker="None",label="Base Plot")
pe = errorbar(x,y,yerr=errs,fmt="o")
axis("tight")
ax = gca() # Get the handle of the current axis
title("Error Bar Scatter")
xlabel("x")
ylabel("y")
grid("on")
gcf()
