require 'html-proofer'

task :test do
  sh "bundle exec jekyll build"
  HTMLProofer.check_directory('_site/', {
    assume_extension: ['.html'],
    ignore_urls: [
      # These urls lead to some errors in html-proofer and were manually checked to be valid
      'https://qcomp.org/benchmarks/index.html#crowds',
      'https://qcomp.org/benchmarks/index.html#jobs',
      'http://fizzed.com/oss/font-mfizz',
      'https://cavconference.org/2017/accepted-papers',
      'https://www.cse.msu.edu/~cse870/Materials/FaultTolerant/manual-galileo.htm#Editing%20in%20the%20Textual%20View',
      'https://getfem.org/gmm.html',
      'https://tempest-synthesis.org',
    ],
  }).run
end
