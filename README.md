GamesCRUD
=========

Clases para el curso SatDev para demostrar lo basico para un proyecto CRUD en ASP.NET

@{
    var NombreJuego = "";
    DateTime ReleaseDate = DateTime.UtcNow;
    var Categoria = "";
    var Text = "";

    if (IsPost)
    {
        NombreJuego = Request["GameName"];
        Categoria = Request["mTitle"];
        Text = Request.Unvalidated("Text");

        Validation.RequireFields("NombreJuego", "Categoria", "Text");
        var SQLINSERT = "INSERT INTO Games (NombreJuego, ReleaseDate, Categoria, Text)VALUES (@0, @1, @2, @3)";
        if (Validation.IsValid())
        {
            try
            {
                var db = Database.Open("StarterSite");
                db.Execute(SQLINSERT, NombreJuego, ReleaseDate, Categoria, Text);
                Response.Write("Datos Guardados!");
            }
            catch (Exception ex)
            {
                Response.Write(ex.Message);
            }
        }
    }
}




<form method="post">
    <fieldset>
        <legend>Insert Data</legend>
        @Html.ValidationSummary(true)
        <div>
            <label>Nombre del Juego</label>
            <input type="text" value="@NombreJuego" name="NombreJuego" />
            @Html.ValidationMessage("NombreJuego")
        </div>

        <div>
            <label>Categoria</label>
            <input type="text" value="@Categoria" name="Categoria" />
            @Html.ValidationMessage("Categoria")
        </div>

        <div>
            <label>Descripcion</label>
            <textarea name="Text">@Text</textarea>
            @Html.ValidationMessage("Text")
        </div>

        <input type="submit" value="Guardar" />
    </fieldset>
</form>


Ejemplo traducido de: http://www.thecodingguys.net/
