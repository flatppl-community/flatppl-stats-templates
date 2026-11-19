# flatppl-stats-templates

[Function reference](docs/reference.md) · [Live example](https://live.flatppl.org/#model=https%3A%2F%2Fraw.githubusercontent.com%2Fflatppl-community%2Fflatppl-stats-templates%2Fmain%2Fexamples%2Fplayground.flatppl&target=Pi_post)

Library **0.1** combines templates and applies a response:

$$f=Ta,\qquad p=R(q\odot f),\qquad H=R\operatorname{diag}(q)T,\qquad Ha=p.$$

Shapes are `T[bins,components]`, `a[components]`, `q[bins]`, and `R[measured,bins]`. Positive quadrature weights $q$ integrate density-valued bins; integrated bins use unit weights. Response losses remain explicit.

```flatppl
flatppl_compat = "0.1"
t = load_module("main.flatppl")
shapes = rowstack([[0.6, 0.1], [0.3, 0.3], [0.1, 0.6]])
means = t.combine(shapes, [25.0, 15.0]) .+ [1.0, 1.0, 1.0]
model = t.poisson_model(shapes, [25.0, 15.0], [1.0, 1.0, 1.0])
log_likelihood = logdensityof(model, [17, 14, 12])
```

Observation laws include independent $N_i\sim\operatorname{Poisson}((Ta+b)_i)$ on nonnegative integer vectors and $Y\sim N(Ta+b,C)$ on real vectors. Poisson means must be nonnegative; $C$ must be positive definite. The reference also covers finite simulation statistics and grid interpolation. No priors, floors, profiling, or extrapolation are implicit.

The [histogram example](examples/histogram-fit.flatppl) exposes component strengths, expected counts, and a log likelihood for host-side optimization.

See the reference for definitions, domains, numerical limits, and validation commands.
