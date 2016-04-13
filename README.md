# PTgen

Create and evaluate probabilistic transcriptions (PT's) of speech recordings
generated by *mismatched crowdsourcing:* by a large number of people
who do not speak the language in those recordings.

The technique is described in this [ICASSP paper](http://www.isle.illinois.edu/sst/pubs/2016/liu16icassp.pdf) and this [AAAI paper](http://www.ifp.illinois.edu/~pjyothi/files/AAAI2015.pdf).

# How to build on Ubuntu

Install [OpenFST](http://www.openfst.org/), [Carmel](http://www.isi.edu/licensed-sw/carmel), and at least the `compute-wer` executable of [Kaldi](https://github.com/kaldi-asr/kaldi).

```
git clone https://github.com/ws15code/PTgen
cd src
make
```

The first time you `make`, you'll be asked to enter the directory of OpenFST's file `fst/compat.h`.
This is usually `/usr/local/include`.  If that fails, `rm config.mk; make`, and instead try a result from the command `locate fst/compat.h`.

# How to create and evaluate PT's

Edit the settings file, e.g. `settings_sample`.
- Ensure that the required files within `$DATA` exist.

`run.sh settings_sample`

If `run.sh` can't find the executable programs of OpenFST, Carmel, or Kaldi, it prompts you for their locations,
and caches your answers in a new file `config.sh`, for future runs.

If you encounter errors and fix them, save time by starting `run.sh` partway through:
change `startstage` to one past the last successfully completed stage.

# How to run prebuilt tests

`cd test/ws15` (or any other test directory).

`../../run.sh settings-foo`

The settings file in each of these tests includes
a `$DATA_URL` for downloading the test's data,
which is too unwieldy to store on github.

If `../../run.sh` prompts you again for the locations of exes, you can just abort it with `ctrl+C`, then retrieve those settings with `cp ../../config.sh .`, then retry.
