# FMOLS

This function carries out Fully Modified Least Squares (FMLS) estimation. It is essentially a translation (with permission) of the Gauss procedure FMPROC included in the suite COINT 2.0, by S. Ouliaris and P.C.B Phillips.

*References*

Hansen, B. E. and P. C. B. Phillips (1990), "Estimation and Inference in Models of Cointegration: A Simulation Study", Advances in Econometrics, Vol. 8, pp. 225-248, Jai Press, Inc.:London.

Phillips, P. C. B. and B. E. Hansen (1990), "Statistical Inference in Instrumental Variables Regression with I(1) Process", Review of Economic Studies 57, pp. 99-125.

# GUI access

The dialog box can be opened via `Model -> Univariate time series -> FMOLS`.


# Public functions

```
FMOLS(const series y, const list x, const bundle opts[null])
```

Conduct estimation.

**Arguments**

- y: series, Dependent variable
- x: list, Right Hand Side I(1) variables
- opts: bundle, Pass user-specific parameters (optional, see below)

**Return:** Bundle holding various items. See below.


The `FMOLS()` function, both in scripting and GUI mode, is executed with some
default parameter values. In GUI mode these can be overridden using the pull-down menus, and in scripting mode by passing the `opts` bundle:

`type_deterministic`

string, Select the deterministic which is believed to be describing the stochastic process of the endogenous.

Options are

- `c`: include a constant (default)
- `ct`: include a constant and linear trend
- `ctt`: include a constant, linear and quadratic trend

`type_dgp_x`

string, Select the deterministic which is believed to be describing the stochastic process of the regressors `x`.

Options are

- `nc`: `x` is assumed to be I(1) with no drift (differences of `x` have zero mean)

- `c`: `x` is assumed to be I(1) with drift (differences of `x` have non-zero mean) (default)

- `ct`: `x` is assumed to be I(1)  with a trending drift (differences of `x` have a trend)


`do_prewhite`:

boolean, Perform VAR(1) pre-whitening when calculating covariances if 1 (=`TRUE`), otherwise not (=`FALSE`). Default is `TRUE`.

`type_kernel`:

string, Select the kernel method. Options are:

- `quadratic`: Quadratic Spectral kernel (default)
- `parzen`: Parzen kernel
- `bartlett`: Bartlett kernel

`bandwidth`:

scalar, Bandwidth for covariance calculation. The special value `-1` (default) triggers Andrews' (1991) automatic bandwidth selection. A VAR(1) model is used to calculate the automatic bandwidth.

`verbose`:
boolean, Print any output if 1 (=`TRUE`, default), otherwise not (=`FALSE`).


*The returned bundle contains*

- `coeff`: matrix, Estimates of the estimated (by FMOLS) long-run coefficients

- `stderr`: matrix, Standard error of the coefficients

- `pvalue`: matrix, P-values of the estimated coefficients

- `vcv`: matrix, Square matrix containing the estimated covariance matrix for the coefficients

- `sigma`: scalar, Standard error of the regression

- `df`: int, Degrees of freedom

- `uhat`: series, Estimated FMOLS-based residuals which are defined as `uhat(t) = y(t) - x(t) x b` where `b` is the vector of long-run coefficients

- `yhat`: series, Fitted values

- `T`: int, Number of valid observations used

- `t1`: int, Index of the initial observation used for estimation

- `t2`: int, Index of the last observation used for estimation

- `depvar`: string, Name of the dependent variable

- `parnames`: strings, Array of names of the exogenous variables

- `names_xlist`: String array of the exogenous

- `aic`: scalar, Akaike information criteria

- `aicc`: scalar, corrected Akaike information criteria

- `bic`: scalar, Schwarz information criteria

- `hqc`: scalar, Hannan-Quinn information criteria

- `bandwidth`: scalar, value of (automatically selected) bandwidth



# Changelog

* **v2.2 (February 2024)**
    * Move help to markdown format
    * Add p-values of coefficient estimates to output bundle
    * Increase minimum version to Gretl 2022a

* **v2.1 (February 2022)**
    * Fix potential bug when computing short-run innovations
    * Put GUI entry under "Univariate time series" menu

* **v2.0 (February 2022)**
    * Refactored code
    * Improved and new user-interface with an option to pass bundle of parameters.
    * Improved printout
    * Return model bundle including various information on estimation

* **v1.0 (March 2017)**
    * initial version
