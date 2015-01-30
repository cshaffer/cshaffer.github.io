require 'date'

task :new_post do
  title = ARGV.last
  post_title = "#{Date.today.to_s}-#{title.downcase.gsub(/[^\w]+/, '-')}"
  post_file = File.dirname(__FILE__) + "/_posts/#{post_title}.md"
  File.open(post_file, "w") do |f|
    f << <<-EOS.gsub(/^    /, '')
    ---
    layout: post
    title: "#{title}"
    date: #{DateTime.now.strftime("%F %T")}
    tags:
    ---
    EOS
  end
  if (ENV['EDITOR'])
    system ("#{ENV['EDITOR']} #{post_file}") 
  end
  task title.to_sym do ; end
end
