---
layout: post
title: Singly Linked List in Ruby
tags: ruby data-structure
---

## Node class

```rb
class Node
  attr_accessor :next
  attr_reader :value

  def initialize(value)
    @value = value
  end
end
```

## Singly Linked List

```rb
class SinglyLinkedList
  attr_reader :head, :tail, :size

  def initialize
    @head = nil
    @tail = nil
    @size = 0
  end

  def add(value)
    node = Node.new(value)
    if @size == 0
      @head = node
    else
      @tail.next = node
    end
    @tail = node
    @size += 1
    true
  end

  def push(value)
    node = Node.new(value)
    node.next = head
    @head = node
    @tail = node if @size == 0
    @size += 1
    value
  end

  def pop
    return if (@size == 0)
    popped_val = head.value
    @head = head.next
    @size -= 1
    @tail = nil if @size == 0
    popped_val
  end

  alias_method :remove, :pop
end
```

## Reference

[3.1 SLList: A Singly-Linked List](https://opendatastructures.org/ods-python/3_1_SLList_Singly_Linked_Li.html)
