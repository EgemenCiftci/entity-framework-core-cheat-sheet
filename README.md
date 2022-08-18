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
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasColumnName("Name");` | Configure a column name. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasDefaultValue("StudentX");` | Configure a column default value. |
| `modelBuilder.Entity<Student>().Property(s => s.LastModified).HasComputedColumnSql("GetUtcDate()");` | Configure a computed column. |
| `modelBuilder.Entity<Student>().Property(s => s.MiddleName).IsRequired(false);` | Configure a null column. |
| `modelBuilder.Entity<Student>().Property(s => s.Surname).IsRequired();` | Configure a not null column. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasMaxLength(50);` | Configure max length for a string column. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).IsUnicode();` | Configure a unicode string column. |


| Usage | Details |
| :--- | :--- |
| `var state = context.Entry<Student>(studentObj).State;` | Get the current state of the entity. |
| `var students = context.Students.FromSqlRaw("SELECT * FROM dbo.Students").ToList();` | Execute raw SQL. |
| `var students = context.Students.FromSqlInterpolated($"SELECT * FROM dbo.Students WHERE NAME={name}").ToList();` | Execute raw SQL with interpolated string. |

