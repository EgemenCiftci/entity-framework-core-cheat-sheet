# Entity Framework Core Cheat Sheet

| Configuration | Details |
| :--- | :--- |
| `modelBuilder.Entity<Student>().ToTable("StudentInfo");` | Map an entity to database table in the default schema. |
| `modelBuilder.Entity<Student>().ToTable("StudentInfo", "dbo");` | Map an entity to database table in a specific schema. |
| `modelBuilder.Entity<Student>().HasKey(s => s.Id);` | Configure primary key(s). |
| `modelBuilder.Entity<Student>().HasAlternateKey(s => s.Id);` | Configure an alternate key. |
| `modelBuilder.Entity<Student>().HasIndex(s => s.Id);` | Configure an index. |
| `modelBuilder.Entity<Student>().HasOne(s => s.Grade);` | Configures the One part of the relationship. |
| `modelBuilder.Entity<Student>().HasMany(s => s.Courses);` | Configures the Many part of the relationship. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasColumnType("varchar");` | Configure a column data type. |


