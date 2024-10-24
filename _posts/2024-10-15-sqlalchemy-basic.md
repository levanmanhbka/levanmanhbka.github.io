---
title: SQLAlchemy 01 - Work With Database
date: 2024-10-15 01:01:01 +0700
categories: [sql alchemy]
tags: [sql orm alchemy]     # TAG names should always be lowercase
---

## 1. What is ORM
ORM (Object-Relational Mapping) là một kỹ thuật lập trình tiên tiến giúp ánh xạ cấu trúc của cơ sở dữ liệu quan hệ phức tạp vào các đối tượng trong phần mềm được viết bằng các ngôn ngữ hướng đối tượng. ORM cung cấp một lớp trừu tượng (abstraction layer) giúp giảm thiểu sự phụ thuộc vào các truy vấn SQL phức tạp, đơn giản hóa việc thao tác với dữ liệu và nâng cao tính bảo trì của code.
- Tables are Classes
- Fields as Attributes
- Rows is Objects

## 2. What is SQLAlchemy ORM
- A Python based Object Relational Mapper
- Talk to SQL Databases from Python programs
- Read, Write, Update, Delete operations

## 3. Sample Code
``` python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker


engine = create_engine("sqlite:///book_store.db")

# Create base class for declarative classes definitions
Base = declarative_base()

# Define class mapped to table
class Book(Base):
    __tablename__ = "book"
    id = Column(Integer, primary_key= True)
    title = Column(String(50))
    author = Column(String(50))

# Drop existing tables if they exist
Base.metadata.drop_all(engine)

# Create all tables in the database
Base.metadata.create_all(engine)

# Create a session for interacting with the database
Session = sessionmaker(bind=engine)

def add_books():
    print("Add books")
    session = Session()
    book1 = Book(title="Book 1", author="Author 1")
    book2 = Book(title="Book 2", author="Author 2")
    session.add_all([book1, book2])
    session.commit()

def get_books():
    print("Get books")
    session = Session()
    books = session.query(Book).all()
    for book in books:
        print(f"ID: {book.id}, Title: {book.title}, Author: {book.author}")

def update_book(old_title, new_title, new_author):
    print("Update book")
    session = Session()
    book = session.query(Book).filter_by(title = old_title).first()
    if book:
        book.title = new_title
        book.author = new_author
        session.commit()
    else:
        print("Book not found")

def delete_book(title):
    print("Delete book")
    session = Session()
    book = session.query(Book).filter_by(title = title).first()
    if book:
        session.delete(book)
        session.commit()
    else:
        print("Book not found")

if __name__ == "__main__":
    add_books()
    get_books()
    update_book("Book 1", "Updated Book 1", "Updated Author 1")
    get_books()
    delete_book("Book 2")
    get_books()
```

## 5. Link Reference
[https://vietnix.vn/orm-la-gi/](https://vietnix.vn/orm-la-gi/)