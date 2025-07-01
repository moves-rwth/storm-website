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
      'https://doi.org/10.1145/2933575.2934574',
      'https://doi.org/10.1609/AAAI.V37I12.26723',
      'https://doi.org/10.1007/s00165-021-00547-2',
      'https://doi.org/10.1609/AAAI.V35I13.17401',
      'http://fizzed.com/oss/font-mfizz', # HTTPS not supported
      'https://github.com/neovim/neovim/issues/9050#issuecomment-424417456', # Anchor not found
      'https://qcomp.org/benchmarks/index.html#crowds', # Anchor not found
      'https://qcomp.org/benchmarks/index.html#jobs', # Anchor not found
      'https://www.rwth-aachen.de/cms/root/Die-RWTH/Aktuell/Pressemitteilungen/Maerz-2021/~mzsyp/Ausgezeichnete-Ideen-fuer-eine-starke-Aa/?lidx=1',
    ],
  }).run
end

task :test_paper_links do
  sh "bundle exec jekyll build"
  HTMLProofer.check_file('paper_links.html', {
    enforce_https: false,
  }).run
end
