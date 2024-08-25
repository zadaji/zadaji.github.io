require 'rake'
require 'yaml'

SOURCE = "."
CONFIG = {
  'posts' => File.join(SOURCE, "_posts"),
  'post_ext' => "md",
}
PICMD_PREFIX = <<-EOS
---
layout: post
title: \"图片帖\"
date: 2024-8-25 
categories: jekyll pics
---
EOS

PICMD_PATH = "./_posts/2025-8-25-pic.md"

# Usage: rake post title="A Title"
desc "Begin a new post in #{CONFIG['posts']}"
task :post do
  abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])
  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['posts'], "#{Time.now.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post

task :pushimg do
  puts "push all imgs."
  files = Dir.glob("./image/*.{png,jpg,jpeg}")
  toMD = PICMD_PREFIX
  files.each do |file|
    toMD = toMD + "![](" + file[1..] + ")\n"
  end
  File.open(PICMD_PATH, "w") do |f|
    f.write(toMD)
  end
  puts "success."
end