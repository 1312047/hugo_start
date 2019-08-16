---
title: "Quy Tắc Viết Code Ruby Có Thể Tốt!"
date: 2019-05-18
draft: false
tags: ["coding", "ruby"]
categories: ["ruby notes"]
mytag: "Ruby"
---

# Đặt vấn đề

Nội dung bài viết là hệ thống lại mốt số cách viết code ruby tốt, phục vụ cho nhu cầu ôn tập của tác giả là chính :smile:  

Vì vậy đây chỉ là một tổng hợp tiếng việt được tham khảo nội dung một cách sâu sắc từ repo [ruby-style-guide](https://github.com/rubocop-hq/ruby-style-guide).

# Luận bàn

# Đặt khoảng trắng  

Đặt khoảng trắng trước và sau toán tử , sau dấu phẩy, dấu hai chấm và dấu chấm phẩy.

```ruby
sum = 1 + 2
a, b = 1, 2
class Cat; end
```

Ngoại lệ liên quan đến các toán tử:  

```ruby
# bad
e = M * c ** 2
# good
e = M * c**2
``` 

KHÔNG DÙNG khoảng trắng sau (, [ hay trước ], ). DÙNG khoảng trắng quanh { và trước }

```ruby
# bad
some( arg ).other
[ 1, 2, 3 ].each{|e| puts e}

# good
some(arg).other
[1, 2, 3].each { |e| puts e }
```

Khi dùng để nhúng vào string, không nên dùng khoảng trắng giữa cặp ngoặc {}.

```ruby
# bad
"From: #{ user.first_name }, #{ user.last_name }"

# good
"From: #{user.first_name}, #{user.last_name}"
```

Không có khoảng trắng sau !.  

```ruby
# bad
! something

# good
!something
```

when và case thụt đầu dòng cùng cấp.  

```ruby
# bad
case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration > 120
    puts 'Too long!'
  when Time.now.hour > 21
    puts "It's too late"
  else
    song.play
end

# good
case
when song.name == 'Misty'
  puts 'Not again!'
when song.duration > 120
  puts 'Too long!'
when Time.now.hour > 21
  puts "It's too late"
else
  song.play
end
```

Thêm một dòng trống giữa các phương thức, và các nhóm xử lý logic.  

```ruby
def some_method
  data = initialize(options)

  data.manipulate!

  data.result
end

def some_method
  result
end
```

Dùng khoảng trắng quanh toán tử = khi gán giá trị mặc định:   

```ruby
# bad
def some_method(arg1=:default, arg2=nil, arg3=[])
  # do something...
end

# good
def some_method(arg1 = :default, arg2 = nil, arg3 = [])
  # do something...
end
```

Tránh dùng dấu ngắt dòng \ khi không bắt buộc. Thực tế, chỉ dùng nó khi cần ngắt dòng string thôi.  

```ruby
# bad
result = 1 - \
         2

# good (but still ugly as hell)
result = 1 \
         - 2

long_string = 'First part of the long string' \
              ' and second part of the long string'
```

Khi gọi phương thức có nhiều đối số.  

```ruby
# mẫu (dòng quá dài)
def send_mail(source)
  Mailer.deliver(to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
end

# bad (thụt đầu dòng hai lần)
def send_mail(source)
  Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text)
end

# good
def send_mail(source)
  Mailer.deliver(to: 'bob@example.com',
                 from: 'us@example.com',
                 subject: 'Important message',
                 body: source.text)
end

# good (thụt đầu dòng bình thường)
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com',
    from: 'us@example.com',
    subject: 'Important message',
    body: source.text
  )
end
```

Nếu mảng có nhiều phần tử.  

```ruby
# bad
menu_item = ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
  'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']

# good
menu_item = [
  'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
  'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam'
]

# good
menu_item =
  ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
   'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']
```

Với số lớn, thêm dấu gạch dưới _ cho dễ đọc.   

```ruby
# bad - có bao nhiêu số `0`?
num = 1000000000

# good - dễ đọc hơn hẳn đúng không :P
num = 1_000_000_000
```

KHÔNG đặt khoảng trắng giữa khối comment và từ khóa def.  

Giới hạn dòng ở 80 ký tự.  

Tránh dùng khoảng trắng thừa (thường gặp ở cuối dòng).   

Cuối file nên có thêm một dòng trống.  

KHÔNG DÙNG block comments.  

***

# Cú pháp / Syntax

KHÔNG sử dụng :: cho các lời gọi hàm thông thường.  

```ruby
# bad
SomeClass::some_method
some_object::some_method

# good
SomeClass.some_method
some_object.some_method
SomeModule::SomeClass::SOME_CONST
SomeModule::SomeClass()
```

Chỉ dùng () khi khai báo phương thức có tham số.  

```ruby
# bad
def some_method()
  # body omitted
end

# good
def some_method
  # body omitted
end

# bad
def some_method_with_parameters param1, param2
  # body omitted
end

# good
def some_method_with_parameters(param1, param2)
  # body omitted
end
```

Nếu phương thức có tham số mặc định, đặt nó ở cuối cùng.  

```ruby
# bad
def some_method(a = 1, b = 2, c, d)
  puts "#{a}, #{b}, #{c}, #{d}"
end

some_method('w', 'x') # => '1, 2, w, x'
some_method('w', 'x', 'y') # => 'w, 2, x, y'
some_method('w', 'x', 'y', 'z') # => 'w, x, y, z'

# good
def some_method(c, d, a = 1, b = 2)
  puts "#{a}, #{b}, #{c}, #{d}"
end

some_method('w', 'x') # => '1, 2, w, x'
some_method('w', 'x', 'y') # => 'y, 2, w, x'
some_method('w', 'x', 'y', 'z') # => 'y, z, w, x'
```

TRÁNH khai báo biến song song.  

```ruby
# bad
a, b, c, d = 'foo', 'bar', 'baz', 'foobar'

# good
a = 'foo'
b = 'bar'
c = 'baz'
d = 'foobar'

# good - hoán đổi giá trị hai biến
a = 'foo'
b = 'bar'

a, b = b, a
puts a # => 'bar'
puts b # => 'foo'

# good - method return
def multi_return
  [1, 2]
end

first, second = multi_return

# good - dùng với splat
first, *list = [1, 2, 3, 4] # first => 1, list => [2, 3, 4]

hello_array = *'Hello' # => ["Hello"]

a = *(1..3) # => [1, 2, 3]
```

Tránh dùng dấu gạch dưới thừa thãi trong khai báo song song.  

```ruby
# bad
foo = 'one,two,three,four,five'
# Phép gán không cần thiết thì không cung cấp bất kỳ thông tin hữu ích nào
first, second, _ = foo.split(',')
first, _, _ = foo.split(',')
first, *_ = foo.split(',')


# good
foo = 'one,two,three,four,five'
# Dấu `_` được dùng khi ta cần lấy hết ra, trừ phần tử cuối cùng.
*beginning, _ = foo.split(',')
*beginning, something, _ = foo.split(',')

a, = foo.split(',')
a, b, = foo.split(',')
# Việc gán cho biến không sử dụng là không cần thiết,
# nhưng nó cung cấp thông tin hữu ích cho ta.
first, _second = foo.split(',')
first, _second, = foo.split(',')
first, *_ending = foo.split(',')
```

Đừng dùng for, trừ khi có lý do chính đáng. Thay vào đó hãy dùng vòng lặp. for là một dạng của each, nhưng for không hỗ trợ scope (each thì có) và biến trong for thì có thể truy cập từ bên ngoài block.  

```ruby
arr = [1, 2, 3]

# bad
for elem in arr do
  puts elem
end

# ra khỏi vòng `for` ta vẫn truy cập biến `elem` được
elem # => 3

# good
arr.each { |elem| puts elem }

elem # => NameError: undefined local variable or method `elem'
```

NÊN dùng toán tử ba ngôi (?:)  

```ruby
# bad
result = if some_condition then something else something_else end

# good
result = some_condition ? something : something_else
```

DÙNG ! thay cho not.   

```ruby
# bad - parentheses are required because of op precedence
x = (not something)

# good
x = !something
```

KHÔNG dùng cặp ngoặc tròn () với if/unless/while/until.  

```ruby
# bad
if (x > 10)
  # body omitted
end

# good
if x > 10
  # body omitted
end
```

Dùng Kernel#loop thay vì while/until khi cần lặp vô hạn.  

```ruby
# bad
while true
  do_something
end

until false
  do_something
end

# good
loop do
  do_something
end
```

Dùng Kernel#loop cùng với break thay vì begin/end/until hay begin/end/while kiểu lặp trước, kiểm tra sau.  

```ruby
# bad
begin
  puts val
  val += 1
end while val < 0

# good
loop do
  puts val
  val += 1
  break unless val < 0
end
```

Nếu hash đã tường minh rồi thì không cần cặp {} nữa.   

```ruby
# bad
user.set({ name: 'John', age: 45, permissions: { read: true } })

# good
user.set(name: 'John', age: 45, permissions: { read: true })
```

Nếu phương thức hệ thống thì có thể bỏ luôn cả () và {}.  

```ruby
class Person < ActiveRecord::Base
  # bad
  validates(:name, { presence: true, length: { within: 1..10 } })

  # good
  validates :name, presence: true, length: { within: 1..10 }
end
```

Nếu block chỉ làm một việc thì ưu tiên dùng shorthand.  

```ruby
# bad
names.map { |name| name.upcase }

# good
names.map(&:upcase)
```

Ưu tiên {...} hơn do...end cho block một dòng. Tránh dùng {...} cho block nhiều dòng. Luôn dùng do...end cho khối điều khiển và khai báo phương thức.   

```ruby
names = %w(Bozhidar Steve Sarah)

# bad
names.each do |name|
  puts name
end

# good
names.each { |name| puts name }

# bad
names.select do |name|
  name.start_with?('S')
end.map { |name| name.upcase }

# good
names.select { |name| name.start_with?('S') }.map(&:upcase)
```

Tránh dùng return, chỉ nên dùng trong luồng điều khiển if..else chẳng hạn.  

```ruby
# bad
def some_method(some_arr)
  return some_arr.size
end

# good
def some_method(some_arr)
  some_arr.size
end
```

Không dùng kết quả của phép gán = trong biểu thức điều kiện.  

```ruby
# bad (+ a warning)
if v = array.grep(/foo/)
  do_something(v)
  # some code
end

# good (MRI would still complain, but RuboCop won't)
if (v = array.grep(/foo/))
  do_something(v)
  # some code
end

# good
v = array.grep(/foo/)
if v
  do_something(v)
  # some code
end
```

Dùng &&= để tiền xử lý biến khi nó có thể tồn tại hoặc không.  

```ruby
# bad
if something
  something = something.downcase
end

# bad
something = something ? something.downcase : nil

# ok
something = something.downcase if something

# good
something = something && something.downcase

# better
something &&= something.downcase
```
Tránh dùng eql?, hãy dùng ==.  

```ruby
# bad - eql? is the same as == for strings
'ruby'.eql? some_str

# good
'ruby' == some_str
1.0.eql? x # eql? makes sense here if want to differentiate between Integer and Float 1
```

Tránh sử dụng các biến đặc biệt kiểu Perl (như $:, $;,.. ).  

```ruby
# bad
$:.unshift File.dirname(__FILE__)

# good
require 'English'
$LOAD_PATH.unshift File.dirname(__FILE__)
```

Lambda không có tham số thì bỏ cặp ngoặc tròn đi.   

```ruby
# bad
l = ->() { something }

# good
l = -> { something }
```

Ưu tiên proc hơn Proc.new.  

```ruby
# bad
p = Proc.new { |n| puts n }

# good
p = proc { |n| puts n }
```

Dùng tiền tố _ cho biến không dùng trong block và biến cục bộ. Hoặc chỉ dùng _ cũng được.  

```ruby
# bad
result = hash.map { |k, v| v + 1 }

def something(x)
  unused_var, used_var = something_else(x)
  # some code
end

# good
result = hash.map { |_k, v| v + 1 }

def something(x)
  _unused_var, used_var = something_else(x)
  # some code
end

# good
result = hash.map { |_, v| v + 1 }

def something(x)
  _, used_var = something_else(x)
  # some code
end
```

Ưu tiên dùng các phương thức có sẵn hơn là so sánh tường minh với ==.  

```ruby
# bad
if x % 2 == 0
end

if x % 2 == 1
end

if x == nil
end

# good
if x.even?
end

if x.odd?
end

if x.nil?
end

if x.zero?
end

if x == 0
end
```

*** 

# Module và Class  

Ưu tiên dùng module_function hơn extend self.  

```ruby
# bad
module Utilities
  extend self

  def parse_something(string)
    # do stuff here
  end

  def other_utility_method(number, string)
    # do some more stuff
  end
end

# good
module Utilities
  module_function

  def parse_something(string)
    # do stuff here
  end

  def other_utility_method(number, string)
    # do some more stuff
  end
end
```

Sử dụng attr.  

```ruby
# bad
class Person
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end

  def first_name
    @first_name
  end

  def last_name
    @last_name
  end
end

# good
class Person
  attr_reader :first_name, :last_name

  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end
end
```

*** 

# Exceptions  

Ưu tiên dùng raise hơn fail.  

```ruby
# bad
fail SomeException, 'message'

# good
raise SomeException, 'message'
```

Tránh dùng từ khoá begin nếu có thể.  

```ruby
# bad
def foo
  begin
    # main logic goes here
  rescue
    # failure handling goes here
  end
end

# good
def foo
  # main logic goes here
rescue
  # failure handling goes here
end
```

Bắt exception theo thứ tự từ thấp đến cao.  

```ruby
# bad
begin
  # some code
rescue StandardError => e
  # some handling
rescue IOError => e
  # some handling that will never be executed
end

# good
begin
  # some code
rescue IOError => e
  # some handling
rescue StandardError => e
  # some handling
end
```

*** 

# Collections  

Ưu tiên khai báo mảng hay hash bằng cặp ngoặc hơn là tạo thể hiện, bởi vì đôi khi ta phải truyền đối số.  

```ruby
# bad
arr = Array.new
hash = Hash.new

# good
arr = []
hash = {}
```

Ưu tiên dùng %W để tạo mảng. Lưu ý chỉ dùng khi mảng có vài phần tử.  

```ruby
# bad
STATES = ['draft', 'open', 'closed']

# good
STATES = %w(draft open closed)
```

Ưu tiên dùng %i nếu muốn tạo mảng các nhãn (symbol).  

```ruby
# bad
STATES = [:draft, :open, :closed]

# good
STATES = %i(draft open closed)
```

Dùng Set thay vì Array khi làm việc với mảng các phần tử độc nhất.  

Khi làm việc với hash, ưu tiên dùng nhãn hơn string khi đặt key.  

```ruby
# bad
hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

# good
hash = { one: 1, two: 2, three: 3 }
```

Dùng Hash#key? thay cho Hash#has_key?, Hash#value? thay cho Hash#has_value? và Hash#each_key thay cho Hash#keys.each, và Hash#each_value thay cho Hash#values.each.    

```ruby
# bad
hash.has_key?(:test)
hash.has_value?(value)

# good
hash.key?(:test)
hash.value?(value)

# bad
hash.keys.each { |k| p k }
hash.values.each { |v| p v }
hash.each { |k, _v| p k }
hash.each { |_k, v| p v }

# good
hash.each_key { |k| p k }
hash.each_value { |v| p v }
```

# Kết luận

Tài liệu tham khảo:  

[https://github.com/rubocop-hq/ruby-style-guide](https://github.com/rubocop-hq/ruby-style-guide)
