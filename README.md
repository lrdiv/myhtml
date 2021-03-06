# MyHTML

[![Build Status](https://travis-ci.org/kostya/myhtml.svg?branch=master)](http://travis-ci.org/kostya/myhtml)

Crystal wrapper for HTML5 Parser https://github.com/lexborisov/myhtml

## Installation


Add this to your application's `shard.yml`:

```yaml
dependencies:
  myhtml:
    github: kostya/myhtml
```

And run `crystal deps`

## Development Setup:

```shell
  git clone https://github.com/kostya/myhtml.git
  cd myhtml
  make

  crystal spec
```


## Usage

```crystal
# Example: print all html tree

require "myhtml"

def walk(node, level = 0)
  puts "#{" " * level}#{node.tag_name}#{node.attributes}(#{node.tag_text.strip})"
  node.children.each { |child| walk(child, level + 1) }
end

str = if filename = ARGV[0]?
        File.read(filename, "UTF-8", invalid: :skip)
      else
        "<html><Div><span class='test'>HTML</span></div></html>"
      end

parser = Myhtml::Parser.new
parser.parse(str)
walk(parser.root!)
```

Output:
```
html{}()
 head{}()
 body{}()
  div{}()
   span{"class" => "test"}()
    -text{}(HTML)
```


## More Examples

[examples](https://github.com/kostya/myhtml/tree/master/examples)

