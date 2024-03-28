---
title: EF Core Very Basic
date: 2024-03-28 01:01:01 +0700
categories: [EF Core]
tags: [efcore]     # TAG names should always be lowercase
---


1. Install EF Core
2. Install EF Core Sqlite

``` c#
// Define Entity
[Table("users")]
public class User
{
    [Column("user_id")]
    public int Id { get; set; }

    [Column("user_name")]
    public string Name { get; set; }
}

// Define database context
public class ShopDBContext : DbContext
{
    public DbSet<User> Users { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlite("Data Source=shop.db");
    }
}

private static void Main(string[] args)
{
    Console.WriteLine("Hello, EF Core!");

    // Create the database if it does not exist
    using(var db = new ShopDBContext())
    {
        db.Database.EnsureCreated();
    }

    // Add user to the database
    using(var db = new ShopDBContext())
    {
        var user_li = new User { Id = 1, Name= "Tran Van Li" };
        var user_luan = new User { Id = 2, Name= "Hoang Thi Luan" };
        db.Users.Add(user_li);
        db.Users.Add(user_luan);
        db.SaveChanges();
    }

    // Show user in database
    using(var db = new ShopDBContext())
    {
        Console.WriteLine("List User:");

        foreach(var user in db.Users)
        {
            Console.WriteLine($"{user.Id} - {user.Name}");
        }
    }
}
```
