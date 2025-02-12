require 'html-proofer'

task :test do
  sh "bundle exec jekyll build"
  HTMLProofer.check_directory('_site/', {
    assume_extension: ['.html'],
    ignore_urls: [
      # These urls lead to some errors in html-proofer and were manually checked to be valid
      'https://www.aachener-zeitung.de/wirtschaft/storm-findet-sicherheitskritische-softwarefehler/3962772.html',
      'https://cavconference.org/2017/accepted-papers', # SSL error
      'https://www.cse.msu.edu/~cse870/Materials/FaultTolerant/manual-galileo.htm#Editing%20in%20the%20Textual%20View', # Anchor not found
      'http://fizzed.com/oss/font-mfizz', # HTTPS not supported
      'https://getfem.org/gmm.html', # SSL error
      'https://qcomp.org/benchmarks/index.html#crowds', # Anchor not found
      'https://qcomp.org/benchmarks/index.html#jobs', # Anchor not found
    ],
  }).run
end

task :test_paper_links do
  sh "bundle exec jekyll build"
  HTMLProofer.check_file('paper_links.html', {
    enforce_https: false,
  }).run
end
