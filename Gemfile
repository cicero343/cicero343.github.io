# frozen_string_literal: true

source "https://rubygems.org"

# Local Jekyll version
gem "jekyll", "~> 4.3.3"

# The default theme for new Jekyll sites. You may change this to anything you like.
gem "minima", "~> 2.5"

# Required for local server on Ruby 3.0+ (already included in newer versions of Jekyll).
gem "webrick", "~> 1.7"

# Jekyll plugins
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-seo-tag"
  gem "jekyll-sitemap"
end

# Windows-specific gems
platforms :mingw, :x64_mingw, :mswin do
  # Performance-booster for watching directories on Windows
  gem "wdm", "~> 0.1.1"
  # tzinfo and tzinfo-data are required for time zone support on Windows
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# JRuby-specific gems
platforms :jruby do
  # Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds
  gem "http_parser.rb", "~> 0.6.0"
end

# Optional: Use GitHub Pages when deploying to GitHub
group :jekyll_plugins do
  gem "github-pages", group: :jekyll_plugins, :platforms => :ruby if ENV["JEKYLL_ENV"] == "production"
end

# Optional: Specify Jekyll version via environment variable (used for CI or specific environments)
# gem "jekyll", ENV["JEKYLL_VERSION"] if ENV["JEKYLL_VERSION"]
# gem "kramdown-parser-gfm" if ENV["JEKYLL_VERSION"] == "~> 3.9"
