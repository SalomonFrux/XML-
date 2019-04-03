using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Data;
using System.Data.SqlClient;
using System.Configuration;

namespace PractiseXMLintoDataBase
{
    public partial class WebForm1 : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            string Scon = ConfigurationManager.ConnectionStrings["MyPractingDataBase"].ConnectionString;
            //string Dcon = ConfigurationManager.ConnectionStrings["DestinationDB"].ConnectionString;

            using (SqlConnection sourceCon = new SqlConnection(Scon))
            {
                DataSet dataSet = new DataSet();
               
                dataSet.ReadXml(Server.MapPath("~/Data.xml"));
                DataTable dataDepartment = dataSet.Tables["Department"];
                DataTable dataEmployee = dataSet.Tables["Employee"];
                using (SqlBulkCopy sqlBulkCopy = new SqlBulkCopy(sourceCon))
                {
                    sqlBulkCopy.DestinationTableName = "Departments";
                    sqlBulkCopy.ColumnMappings.Add("ID", "ID");
                    sqlBulkCopy.ColumnMappings.Add("Name", "Name");
                    sqlBulkCopy.ColumnMappings.Add("Location", "Location");

                    sourceCon.Open();
                    sqlBulkCopy.WriteToServer(dataDepartment);
                }

                using (SqlBulkCopy sqlBulkCopy = new SqlBulkCopy(sourceCon))
                {
                    sqlBulkCopy.DestinationTableName = "NewEmployees";
                    sqlBulkCopy.ColumnMappings.Add("ID", "ID");
                    sqlBulkCopy.ColumnMappings.Add("Name", "Name");
                    sqlBulkCopy.ColumnMappings.Add("Gender", "Gender");
                    sqlBulkCopy.ColumnMappings.Add("DepartmentId", "DepartmentId");

                    sqlBulkCopy.WriteToServer(dataEmployee);
                }
                //    string SourcecmdText = "SELECT * FROM Departments";
                //SqlCommand cmd = new SqlCommand(SourcecmdText, sourceCon);
            }
            
        }
    }
}
