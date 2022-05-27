# Stan Model Server

A lightweight server interface to Stan model methods.

#### Installation Instructions

For installation instructions, see

* Installing Stan Model Server [Install Documentation](doc/INSTALL.md)

#### Read-Eval-Print Loop

For full documentation on the REPL, see:

* Stan Model Server [REPL Documentation](doc/REPL.md)


## Hello, Shell!

The package is distributed with a a Stan program in
`stan/bernoulli/bernoulli.hpp` and matching data in
`stan/bernoulli/bernoulli.data.json`.

> Before trying this, check out the [dependencies](#Dependencies)
section below.

To compile the server
executable,

```
$ cd stan-model-server
$ make CMDSTAN=/Users/carp/github/stan-dev/cmdstan stan/bernoulli/bernoulli
```

Then we run from the command line with data and an RNG seed.

```
$ stan/bernoulli/bernoulli -s 1234 -d stan/bernoulli/bernoulli.data.json
```

The lines marked with `<` indicate input from the user and those with
`>` the response from the server.

```
< name
bernoulli_model

< param_num 1 1
3

< param_unc_num
1

< param_names 1 1
theta,logit_theta,y_sim

< param_unc_names
theta

< param_constrain 1 1 -2.3
0.0911229610148561,-2.3,0

< param_unconstrain {"theta":0.09112}
-2.30003575312272

< log_density 1 1 1 1 -1.5
-6.91695933579303,0.810893714323724,-1.78975742485563
```


## Motivation and Inspiration

We want to be able to access Stan model methods from within R or
Python in order to do algorithm development.  The original system that
did this is the HTTPStan, which is an official Stan project

* GitHub stan-dev: [httpstan](https://github.com/stan-dev/httpstan)

The direct inspiration for this project came from Redding Stan, by
Daniel Lee and Dan Muck.

* Dan Muck and Daniel
  Lee. 2022. [Smuggling log probability and gradients out of Stan programs — ReddingStan](https://blog.mc-stan.org/2022/03/24/smuggling-log-probability-and-gradients-out-of-stan-programs-reddingstan/). *The
  Stan Blog*.
* dmuck. [redding-stan](https://github.com/dmuck/redding-stan). GitHub.


## Python Client

The Python client is still a work in progress and so far only has the
`name()` method implemented.

```python
> import StanModelClient
> s = StanModelClient.StanClient("./bernoulli", data = "bernoulli.data.json", seed = "1234")
> s.name()
bernoulli_model
```


## License

* Code released under the [BSD-3 license](LICENSE).
* Documentation released under the
  [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/).
