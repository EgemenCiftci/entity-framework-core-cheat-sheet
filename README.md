# Entity Framework Core Cheat Sheet (EF Core 6.0)

| Configuration | Details |
| :--- | :--- |
| `modelBuilder.HasDefaultSchema("dbo");` | Set default schema. |
| `modelBuilder.Entity<Student>().ToTable("StudentInfo");` | Map an entity to database table in the default schema. |
| `modelBuilder.Entity<Student>().ToTable("StudentInfo", schema: "dbo");` | Map an entity to database table in a specific schema. |
| `modelBuilder.Entity<Student>().ToView("StudentsView", schema: "dbo");` | Map an entity to database view in a specific schema. |
| `modelBuilder.Entity<Student>().HasKey(s => s.Id);` | Configure primary key(s). |
| `modelBuilder.Entity<Student>().HasAlternateKey(s => s.Id);` | Configure alternate key(s). |
| `modelBuilder.Entity<Student>().HasIndex(s => s.Id);` | Configure index(es). |
| `modelBuilder.Entity<Student>().HasIndex(s => s.Id).IsUnique();` | Configure unique index(es). |
| `modelBuilder.Entity<Student>().HasIndex(s => s.Url).HasDatabaseName("Index_Url");` | Configure index name. |
| `modelBuilder.Entity<Student>().HasIndex(s => s.Url).HasFilter("[Url] IS NOT NULL");` | Configure index filter. |
| `modelBuilder.Entity<Student>().HasOne(s => s.Grade);` | Configures the One part of the relationship. |
| `modelBuilder.Entity<Student>().HasMany(s => s.Courses);` | Configures the Many part of the relationship. |
| `modelBuilder.Entity<Student>().HasComment("Some comment");` | Set text comment in the database. |
| `modelBuilder.Entity<Student>().Ignore(s => s.LoadedFromDatabase);` | Exclude a property. |
| `modelBuilder.Entity<Product>().HasCheckConstraint("CK_Prices", "[Price] > [DiscountedPrice]", c => c.HasName("CK_Product_Prices"));` | Configure check constraint. |
| `modelBuilder.HasSequence<int>("OrderNumbers");`<br/>`modelBuilder.Entity<Order>().Property(o => o.OrderNo).HasDefaultValueSql("NEXT VALUE FOR OrderNumbers");` | Configure a sequence. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasColumnType("varchar(200)");` | Configure a column data type. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasColumnName("Name");` | Configure a column name. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasDefaultValue("StudentX");` | Configure a column default value. |
| `modelBuilder.Entity<Student>().Property(s => s.Created).HasDefaultValueSql("getdate()");` | Configure a column default value by SQL. |
| `modelBuilder.Entity<Student>().Property(s => s.LastModified).HasComputedColumnSql("GetUtcDate()");` | Configure a computed column. |
| `modelBuilder.Entity<Student>().Property(s => s.LastModified).HasComputedColumnSql("GetUtcDate()", stored: true);` | Configure a stored computed column. |
| `modelBuilder.Entity<Student>().Property(s => s.Surname).IsRequired();` | Configure a not null column. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasMaxLength(50);` | Configure max length for a string or array type column. |
| `modelBuilder.Entity<Student>().Property(s => s.Weight).HasPrecision(5, 2);` | Configure precision and scale of the type. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).IsUnicode(false);` | Configure a non-Unicode string column. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).UseCollation("SQL_Latin1_General_CP1_CI_AS");` | Configure collation of a text column. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasComment("Some comment");` | Set a column comment. |
| `modelBuilder.Entity<Student>().Property(s => s.Name).HasColumnOrder(1);` | Set column order. |
| `modelBuilder.Entity<Student>().Property(s => s.Inserted).ValueGeneratedOnAdd();` | Set value generation for a column on add. |
| `modelBuilder.Entity<Student>().Property(s => s.LastUpdated).ValueGeneratedOnAddOrUpdate();` | Set value generation for a column on add or update. |
| `modelBuilder.Entity<Student>().Property(s => s.Id).ValueGeneratedNever();` | Disable value generation. |
| `modelBuilder.Entity<Student>().Property(s => s.LastName).IsConcurrencyToken();` | Configure a concurrency token. |
| `modelBuilder.Entity<Student>().Property(s => s.Timestamp).IsRowVersion();` | Configure a property to be a timestamp/rowversion. |
| `modelBuilder.Entity<Student>().Property<DateTime>("LastUpdated");` | Configure a shadow property. |
| `modelBuilder.Entity<Student>().IndexerProperty<DateTime>("LastUpdated");` | Configure an indexer property. |

| Usage | Details |
| :--- | :--- |
| `using var context = new SchoolContext();`<br/>`// Work with context here` | Create and use a database context. |
| `context.Add(new Student { Name = "SomeName" });`<br/>`context.SaveChanges();` | Create. |
| `var entity = context.Students.FirstOrDefault(f => f.Name == "SomeName");` | Read. |
| `entity.Surname = "SomeSurname"`<br/>`context.SaveChanges();` | Update. |
| `context.Delete(entity);`<br/>`context.SaveChanges();` | Delete. |
| `var state = context.Entry<Student>(entity).State;` | Get the current state of the entity. |
| `var students = context.Students.FromSqlRaw("SELECT * FROM dbo.Students").ToList();` | Execute raw SQL. |
| `var students = context.Students.FromSqlInterpolated($"SELECT * FROM dbo.Students WHERE NAME={name}").ToList();` | Execute raw SQL with interpolated string. |

