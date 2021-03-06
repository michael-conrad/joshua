Apache Joshua 6.1 (Jan 26th, 2017)
==================================
Release Report - https://s.apache.org/joshua6.1

Sub-task

    [JOSHUA-301] - Add findbugs plugin to maven build

Bug

    [JOSHUA-22] - Parallelize MBR computation
    [JOSHUA-71] - OS X installation depends on coreutils to run thrax test
    [JOSHUA-95] - Vocabulary locking
    [JOSHUA-107] - Verbosity levels
    [JOSHUA-172] - Speed up grammar file reading with memory-mapped files
    [JOSHUA-239] - Dependency addition to Joshua-Decoder/Joshua/pom.xml
    [JOSHUA-259] - Integration tests are failing
    [JOSHUA-268] - Phrase-based model error (NullPointerException)
    [JOSHUA-271] - Thrax invocation should not reply upon $HADOOP being set
    [JOSHUA-276] - Trivial fixes to 1.8 Javadoc
    [JOSHUA-278] - Alignments printed incorrectly for phrase-based decoder
    [JOSHUA-279] - Cannot build Joshua master branch
    [JOSHUA-280] - Existing Language packs not compatible with Joshua master
    [JOSHUA-281] - split2files.pl support script no longer exists hence pipeline fails
    [JOSHUA-282] - %S output format doesn't remove <s>
    [JOSHUA-284] - Phrase-based decoding changes
    [JOSHUA-285] - Not all RuntimeExceptions are caught
    [JOSHUA-287] - KenLM.java catches UnsatisfiedLinkError when attempting to load libken.so (libken.dylib on OSX)
    [JOSHUA-299] - Move regression tests to proper unit tests
    [JOSHUA-304] - word-align.conf alignment template file not compatible with berkeley aligner
    [JOSHUA-305] - joshua-6.1-SNAPSHOT-source-release.zip takes ages to build
    [JOSHUA-319] - test-decode decoder_command results in java.lang.NumberFormatException: For input string: "MAXSPAN"
    [JOSHUA-321] - Add JOSHUA env to ./bin/bleu and ./bin/extract-1best bash scripts
    [JOSHUA-322] - extract-1best script references non-existent execution paths

Improvement

    [JOSHUA-252] - Make it possible to use Maven to build Joshua
    [JOSHUA-256] - Note that Joshua builds and runs with >= Java 1.8
    [JOSHUA-262] - Implement all logging as Slf4j over Log4j
    [JOSHUA-269] - Fix Javadoc in JOSHUA-252 branch to comply with JDK1.8 Spec
    [JOSHUA-272] - Simplify the packing and usage of phrase-based grammars
    [JOSHUA-286] - Remove presence of all joshua-decoder.org links in codebase
    [JOSHUA-291] - Improve code quality via static analysis
    [JOSHUA-296] - Refactor threading code
    [JOSHUA-309] - Update CHANGELOG
    [JOSHUA-312] - Even though alignment is cached, it is always re-done in pipeline re-execution

New Feature

    [JOSHUA-100] - Add Shen et al. (2008) dependency LM

Task

    [JOSHUA-248] - Add Apache License headers to Joshua code
    [JOSHUA-249] - Joshua Logo
    [JOSHUA-251] - Address Website Branding Issues
    [JOSHUA-254] - Update README with correct branding
    [JOSHUA-255] - License headers for all bash scripts
    [JOSHUA-257] - Add license headers to all Python scripts
    [JOSHUA-258] - Add back penn-treebank-(de)tokenizer perl scripts
    [JOSHUA-261] - Remove ext directory from source tree
    [JOSHUA-297] - List supported versions of Hadoop
    [JOSHUA-323] - Joshua 6.1 Release Management

Test

    [JOSHUA-253] - Enable execution of Unit tests
	
6.0.5 (October 23, 2015)
========================

- KenLM updated, includes vastly improved cmake-based build
- Fix for grammar packing that previously limited the size of grammars (esp. Hiero)
- Support for packing and decoding with multiple packed grammars (if packed together)
- Feature functions now report dense features, for more efficient handling
- Added AdaGrad and internal MIRA
- Pipeline:
  - Alignment of different chunks now parallelized
  - Computes meteor scores if $METEOR is defined
  - Updated to use Hadoop 2.5.2
  - Reworked how multiple tuning runs (for optimizer instability) function 
- Maven compatibility
- Developers
  - Ant eclipse target
  - Added code formatting spec for Eclipse import
- Many bugfixes and other improvements

6.0.4 (June 15, 2015)
=====================

- Local MIRA implementation (now the default for the pipeline; Moses' kbmira available
  with '--tuner kbmira')
- PRO tuning implementation restored
- Alignment in pipeline parallelized across chunks (up to --threads)
- Better integration for class-based LMs
- Bugfixes in pipeline script and elsewhere
- Logic for KenLM/lmplz boost compile improved

6.0.3 (June 1, 2015)
====================

- New, more versatile run bundler for creating language packs
- Restructuring of the pipeline. Now uses the run bundler to build models
  for tuning and testing, and no longer directly supports multiple optimizer
  runs
- Split out ZMERT / PRO tuning script into run_zmert.py, to facilitate 
  running ZMERT independently
- Fix to ivy (dependency download tool) for offline and cached downloads
- Other bug fixes and changes

6.0.2 (April 10, 2015)
======================

- Restored compatibility with Moses 3.0 tuning regime (tuning with kbmira 
  now requires Moses 3.0)
- Sparse feature support in grammar file, which enables compatibility with 
  PPDB grammars (paraphrase.org)
- Bugfixes and other minor improvements

6.0.1 (March 6, 2015)
=====================

Bugfixes:

- Maximum phrase length was off by one (short)

Improvements

- **Phrase-table packing for Moses grammars**
- BerkeleyLM now detects compressed files automatically
- output-format now respected when top-n = 0 (with a subset of variables)
- key + value format for specifying TMs
- Better error messages and other minor improvements	
	
6.0 (February 4, 2015)
======================

Joshua 6.0 introduces many extensions and improvements. They include:

- Phrase-based decoder

  Joshua now includes an unlexicalized phrase-based decoder. It reads
  Moses phrase tables directly. Support for training phrase-based
  models is included in the pipeline (via callouts to Moses)

- Significant speed improvements

  Joshua is a lot faster (TODO: quantify). The phrase-based decoder is
  on roughly par with Moses in terms of decoding speed: slower for
  small beam sizes and faster for larger (above 200). GHKM decoding is
  significantly faster as a result of the dot chart removal due to
  Sennrich (2014).

- Numerous bugfixes and other improvements

  Dynamic lattice-based OOV segmenting, improved progress meters and
  verbose output handling, support for alignments in phrase table,
  latest KenLM (including lmplz)
	
5.0 (August 16, 2013)
===================

The main features of this release are described in

  "Joshua 5.0: Sparser, Better, Faster, Server"
  Matt Post, Juri Ganitkevitch, Luke Orland, Jonny Weese, Yuan Cao, and Chris Callison-Burch. 
  ACL Workshop on Statistical Machine Translation. August, 2013.
  www.statmt.org/wmt13/pdf/WMT26.pdf

- Sparse feature implementation

  Joshua now uses sparse features natively, with support for (hundreds of) thousands of
  features and large-scale discriminative tuning via PRO (included) or kbMIRA (via Moses).

- Significant performance improvements

  Joshua is up to 6 times faster than the previous release. It scales to many threads
  easily, and the packed grammar and amortized sorting virtually remove model loading times.

- Added left-state LM minimization support (via KenLM)

  Tests show that Joshua has parity with Moses in terms of speed and search.

- Thrax 2.0

  Thrax 2.0 is significantly faster, uses less disk space, and has been tested on corpora
  of one hundred million sentence pairs.

- Server

  Joshua now includes a multithreaded TCP/IP server with round-robin scheduling among
  connections.

- Many, may bugfixes


4.0 (July 2, 2012) 
==================

The main features of this release are described in 

  "Joshua 4.0: Packing, PRO, and Paraphrasing."
  Juri Ganitkevitch, Yuan Cao, Jonny Weese, Matt Post, and Chris Callison-Burch. 
  NAACL Workshop on Statistical Machine Translation, June, 2012.

They include:

- Significantly improved and expanded documentation (both user and developer)

  See http://joshua-decoder.org/4.0 or ./joshua-decoder.org/4.0/index.html (local mirror)

- Synchronous parsing

  Joshua will compute the best synchronous derivation over a pair of
  sentences.  Pass the sentences in in the form 

    source sentence ||| target sentence

  and set the parameter "parse = true" (either from the config file or
  command-line).

- PRO implementation

  We include an implementation of Pairwise Ranking Optimization (PRO,
  Hopkins & May, EMNLP 2011).  It can be activated by passing "--tuner
  pro" to the pipeline script.

- Grammar packing

  We include an efficient grammar representation that can be used to
  greatly reduce the memory footprint of large grammars.

- Numerous bugfixes

== 3.2 (February 17, 2012) ======================================

- Pop-limit pruning.

  Pruning can now be specified with a single parameter "pop-limit"
  parameter, which limits the number of pops from the cube pruning
  candidate list at the span level.  This replaces the beam and
  threshold pruning that was governed by four parameters (fuzz1,
  fuzz2, relative_threshold, and max_n_rules), whose performance and
  interaction was somewhat difficult to characterize.  The pop-limit
  allows a simple relationship between decoding time and model score
  to be defined.

  Setting "pop-limit" in the configuration file or from the command
  line turns off beam-and-threshold pruning, and its use is
  recommended.  The default setting is to use a pop-limit of 100.

- Multiple language model support

  You can now specify an arbitrary number of language models.  See the
  documentation in

    $JOSHUA/scripts/training/templates/mert/joshua.config 

  for information on how to do this.  You can also specify multiple
  --lmfile flags to the pipeline.pl script.

- Multiple optimizer + test runs (--optimizer-runs N), averaging the
  results at the end (Clark et al., ACL 2011)

- Added support for BerkeleyLM (Pauls and Klein, ACL 2011)

- Support for lattice decoding (thanks to Lane Schwartz and the
  miniSCALE 2012 team)

- Pipeline script:

  - Removed all external dependencies (e.g., Moses, SRILM)

  - Reorganized the training data

  - Permit multiple test runs with subsequent --test FILE --name NAME
    calls to the pipeline

  - GIZA++ runs are parallelized if more than one thread is permitted
    (--threads N, N >=2 )

  - Numerous bugfixes

  - Hadoop cluster rollout is now a single instance (slower but
    doesn't require error-prone server setup)

- Parameters

  - Joshua now dies if it encounters unknown parameters on the command
    line or config file

  - Parameters are now normalized to remove hyphens (-) and
    underscores (_) and to flatten case, permitting you to specify any
    of, for example, {pop-limit, popLimit, pop_limit, ...}

- Lots of reorganization and purging of old code


3.1 
=============================

- Fixed multithreading.  Use -threads N from the command line or
  configuration file to spawn N parallel decoding threads.

- Configuration file parameters can now be overridden from the command
  line.  The format is

  -parameter value

  Among these must be the configuration file itself, which can be
  referred to with -config, or -c for short.

3.0
===

- Added the highly parameterizable Hadoop-based Thrax grammar
  extractor, which extracts both Hiero and SAMT grammars.

- Incorporated a black-box pipeline script at
  $JOSHUA/scripts/training/pipeline.pl

- Moved development to github.com.
