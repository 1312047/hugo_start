---
title: "Bài toán brackets"
date: 2019-07-11
draft: false
tags: ["Programming"]
categories: ["algo"]
mytag: "Algo"
---

## Yêu cầu

### Input

Đầu vào là 1 chuỗi chỉ chứa các ký tự nằm trong mảng sau:  

```ruby
['{', '}', '[', ']', '(', ')']
```

Ex: `"{{}}"`, `"[(})"` ... 

### Output

Trả về kết quả liệu chuỗi đầu vào có phải là một brackets hợp lệ hay không.  

:arrow_right: Một chuỗi hợp lệ là một chuỗi dấu ngoặc có thể sử dụng trong một phép toán hợp lệ.  

Ex:  

`"()()"` là hợp lệ.  
`"({()()})"` là hợp lệ.  
`"{)"` không hợp lệ.  
`"()([})"` không hợp lệ.  

## Giải pháp

### Ý tưởng

Xây dựng giải pháp trên cơ chế `stack`. Nếu gặp ký tự mở (`{`, `[`, `(`) thì bỏ vào stack, nếu gặp ký tự đóng (`}`, `]`, `)`) thì pop phần tử trong stack ra so sánh. Nếu phần tử được pop từ stack với ký tự đang so sánh tạo thành được 1 cặp dấu hợp lệ (`()`, `[]`, `{}`) thì duyệt tiếp, nếu không tạo thành cặp dấu hợp lệ thì trả về false, vì đây không phải chuỗi brackets valid.  

### Implement

```ruby
# so sánh 2 ký tự có tạo thành 1 cặp dấu hợp lệ hay không
def compare(x , y)
  if x == '{'
    return true ? y == '}' : false
  end

  if x == '('
    return true ? y == ')' : false
  end

  if x == '['
    return true ? y == ']' : false
  end
end

# duyệt chuỗi
def is_backet?(str)
  str.split
  arr = []
  open_str = ['{', '[', '(']
  str.size.times do |x|
    if open_str.include? str[x]
      arr.push(str[x])
    else
      if !compare arr.pop, str[x]
        return false
      end
    end
  end
  true
end
```
