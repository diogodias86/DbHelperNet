# DbHelperNet

Examples

    private DbHelper dbHelper = new DbHelper();

    public Model LoadById(Guid id)
    {
        var sql = $"SELECT * FROM table WHERE id = @id";

        var parms = new object[]
        {
            "@id", id
        };

        return dbHelper.Read<Model>(sql, Mapper, parms).FirstOrDefault();
    }

    public void Save(Model model)
    {
        var sql = $"UPDATE table SET field_1 = @field_1 WHERE id = @id";

        var parms = new object[]
        {
            "@id", model.Id,
            "@field_1", model.Field1
        };

        dbHelper.Update(sql, parms);
    }

    private static Func<IDataReader, model> Mapper = reader =>
        new Model
        {
            Field1 = reader["field_1"].AsGuid(),
            Field2 = reader["field_2"].AsString(),
            Field3 = reader["field_3"].AsString(),
            Field4 = reader["field_4"].AsByteArray()            
        };
