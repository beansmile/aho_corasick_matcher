# Aho-Corasick Matcher [![Build Status](https://travis-ci.org/altmetric/aho_corasick_matcher.svg?branch=master)](https://travis-ci.org/altmetric/aho_corasick_matcher)

**fork from [altmetric/aho_corasick_matcher](https://github.com/altmetric/aho_corasick_matcher)**

A Ruby gem for finding strings in text using the [Aho-Corasick string matching search](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.96.4671&rep=rep1&type=pdf).

Aho-Corasick is `O(n + m)` where `n` is the size of the string to be searched
and `m` is the size of the dictionary. This means it's particularly suited for
searching for occurrences of words using large dictionaries, as the runtime
increases only linearly.

It's quite memory-intensive, and building a matcher is expensive – but once it's
been built, matching terms is very fast.

**Current version:** 1.0.2  
**Supported Ruby versions:** 1.8.7, 1.9.2, 1.9.3, 2.0, 2.1, 2.2, jruby-1.7, rbx-2.5

## Usage

```ruby
require 'aho_corasick_matcher'
require 'aho_corasick_matcher_error'

matcher = AhoCorasick::AhoCorasickMatcher.new(['a', 'b', 'ab'])
matcher.match('aba')
#=> ['a', 'ab', 'b', 'a']

matcher = AhoCorasickMatcher.new(['thistle', 'sift', 'thistles'])
matcher.match('Theophilus thistle, the successful thistle sifter, in sifting a sieve full of un-sifted thistles, thrust three thousand thistles through the thick of his thumb.')
#=> ["thistle", "thistle", "sift", "sift", "sift", "thistle", "thistles", "thistle", "thistles"]
```

or use the `runner` if we don't need to initialize a new matcher everytime

```ruby
require 'aho_corasick_matcher'
require 'aho_corasick_matcher_error'

# AhoCorasick::AhoCorasickMatcher.runner('new dictionary string')
matcher1 = AhoCorasick::AhoCorasickMatcher.runner('a b ab')
matcher2 = AhoCorasick::AhoCorasickMatcher.runner

matcher1.match('aba')
#=> ['a', 'ab', 'b', 'a']

matcher2.match('aba')
#=> ['a', 'ab', 'b', 'a']
```

## Thanks

Loosely based on [Tim Cowlishaw's implementation of the same algorithm](https://github.com/timcowlishaw/aho_corasick).

## License

Copyright © 2015-2016 Altmetric LLP

Distributed under the MIT License.
