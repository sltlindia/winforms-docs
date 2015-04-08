---
title: Mail Merge
page_title: Mail Merge
description: Mail Merge
slug: richtexteditor-features-mail-merge
tags: mail,merge
published: True
position: 13
---

# Mail Merge



The general use of mail merge is the creation of a document serving as a template and filling in different data, e.g. the name of a person, their address,
        job title, etc. However, mail merge can be used in other scenarios as well, when some part of the document will be repeated several times with slight alterations.
        The template which stays mostly unchanged in all records is regarded as "Main Document". In addition to the static content, it also contains placeholders – "Merge Fields" –
        which represent the variable data and are replaced with the actual content upon performing the mail merge. The information used for filling up the Merge Fields is kept
        separately and is called "Data Source".
      

## Setting up the Data Source

The first thing you need to do is assign a value to the __ItemsSource__ property of the __MailMergeDataSource__ of the document. For example, if you will be writing letters to
          Employees of a company, you can have a context which keeps a list of Employees, each Employee having a FirstName, LastName and JobTitle.
        

#### __[C#] __

{{region data}}
	            
	    public class ExamplesDataContext
	    {
	        private List<Employee> employees = new List<Employee>()
	        {
	            new Employee()
	            {
	                FirstName = "Andrew",
	                LastName = "Fuller",
	                JobTitle = "Director - Finance",
	            },
	            new Employee()
	            {
	                FirstName = "Nancy",
	                LastName = "Davolio",
	                JobTitle = "Director - Human Resources",
	            },
	            new Employee()
	            {
	                FirstName = "Robert",
	                LastName = "King",
	                JobTitle = "Engineering Design Manager",
	            },
	            new Employee()
	            {
	                FirstName = "Margaret",
	                LastName = "Peacock",
	                JobTitle = "Finance & Investments Officer",
	            }
	        };
	        
	        public List<Employee> Employees
	        {
	            get
	            {
	                return this.employees;
	            }
	        }
	    }
	
	    public class Employee
	    {
	        public string FirstName { get; set; }
	
	        public string LastName { get; set; }
	
	        public string JobTitle { get; set; }
	    }
	
	{{endregion}}



#### __[VB.NET] __

{{region data}}
	
	Public Class ExamplesDataContext
	
	    Private _employees As New List(Of Employee)() From {
	        New Employee() With {.FirstName = "Andrew", .LastName = "Fuller", .JobTitle = "Director - Finance"},
	        New Employee() With {.FirstName = "Nancy", .LastName = "Davolio", .JobTitle = "Director - Human Resources"},
	        New Employee() With {.FirstName = "Robert", .LastName = "King", .JobTitle = "Engineering Design Manager"},
	        New Employee() With {.FirstName = "Margaret", .LastName = "Peacock", .JobTitle = "Finance & Investments Officer"}
	    }
	
	    Public ReadOnly Property Employees() As List(Of Employee)
	        Get
	            Return Me._employees
	        End Get
	    End Property
	End Class
	
	Public Class Employee
	    Public Property FirstName() As String
	
	    Public Property LastName() As String
	
	    Public Property JobTitle() As String
	End Class
	
	#End Region



All that is left is to add the following line:

#### __[C#] __

{{region source}}
	            
	            this.radRichTextEditor1.Document.MailMergeDataSource.ItemsSource = new ExamplesDataContext().Employees;
	            
	{{endregion}}



#### __[VB.NET] __

{{region source}}
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.ItemsSource = (New ExamplesDataContext()).Employees
	
	        '#End Region
	
	        '#Region "field"
	
	        Dim field As New MergeField() With {.PropertyPath = "FirstName"}
	
	        '#End Region
	
	        '#Region "mode"
	
	        field.DisplayMode = FieldDisplayMode.Result
	
	        Me.radRichTextEditor1.Document.ChangeFieldDisplayMode(field.FieldStart, FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.ChangeFieldDisplayMode(field.FieldStart, FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.Document.ChangeAllFieldsDisplayMode(FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.ChangeAllFieldsDisplayMode(FieldDisplayMode.Result)
	
	        '#End Region
	
	        '#Region "insert"
	
	        Me.radRichTextEditor1.InsertField(field)
	
	        Me.radRichTextEditor1.InsertField(field, FieldDisplayMode.DisplayName)
	
	        '#End Region
	
	        '#Region "preview"
	
	        Me.radRichTextEditor1.PreviewFirstMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewLastMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewMailMergeDataRecordAtIndex(0)
	
	        Me.radRichTextEditor1.PreviewNextMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewPreviousMailMergeDataRecord()
	
	        '#End Region
	
	        Dim index As Integer = 0
	
	        '#Region "perform"
	
	        Me.radRichTextEditor1.MailMergeCurrentRecord() ' returns a RadDocument that is the result of substituting the merge fields with the data from the current record. The current record can be specified through the MailMergeSource API:</para>
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToFirst()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToLast()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToNext()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToPrevious()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToIndex(index)
	
	        Me.radRichTextEditor1.MailMerge(False) ' returns a RadDocument that is the result of Mail Merging all records. The parameter specifies if a page break should be inserted between the records (default value is true).
	
	        '#End Region
	    End Sub
	End Class
	
	#Region "data"
	
	Public Class ExamplesDataContext
	
	    Private _employees As New List(Of Employee)() From {
	        New Employee() With {.FirstName = "Andrew", .LastName = "Fuller", .JobTitle = "Director - Finance"},
	        New Employee() With {.FirstName = "Nancy", .LastName = "Davolio", .JobTitle = "Director - Human Resources"},
	        New Employee() With {.FirstName = "Robert", .LastName = "King", .JobTitle = "Engineering Design Manager"},
	        New Employee() With {.FirstName = "Margaret", .LastName = "Peacock", .JobTitle = "Finance & Investments Officer"}
	    }
	
	    Public ReadOnly Property Employees() As List(Of Employee)
	        Get
	            Return Me._employees
	        End Get
	    End Property
	End Class
	
	Public Class Employee
	    Public Property FirstName() As String
	
	    Public Property LastName() As String
	
	    Public Property JobTitle() As String
	End Class
	
	#End Region



## Performing Mail Merge

MailMerge can be done both [using the UI](#mailmerging-using-the-ui:)
          and [programmatically.](#programmatic-mail-merge)

### MailMerging using the UI:

RadRichTextEditor comes with a predefined UI for inserting merge fields, previewing the results and fulfilling the merge. It is separated in the
              Mailings tab:
            ![richtexteditor-features-mail-merge 001](images/richtexteditor-features-mail-merge001.png)

The options in the drop down button InsertMergeField are automatically populated to match the properties of the objects which are used as data source.
              You can also switch the display mode of the merge fields from FieldCodes (as in the picture) to FieldNames (e.g. “<<FirstName>>”) or preview the results.
            

If you click the "Preview Results" button, the fields will be replaced with the data from the current record, which by default is the first item from the data
              source. Then, you can further iterate through the records using the First, Last, Previous and Next buttons.
            

If you wish to save the document as a template, you can do so by executing the SaveFileCommand from the application menu in the ribbon bar. 

>The merge fields are persisted only in XAML and docx.

In the end, you can fulfill the mail merge from the MailMerge button, which executes the MailMergeCommand. A SaveFileDialog dialog will pop up prompting you to
              choose where you wish to save the document – result of mail merge and in what file format.
            



### Programmatic Mail Merge

This same scenario can be carried out programmatically just as easily. The methods that can be used are:
            

### Creating a MergeField:



#### __[C#] __

{{region field}}
	            
	            MergeField field = new MergeField() { PropertyPath = "FirstName" };
	
	{{endregion}}



#### __[VB.NET] __

{{region field}}
	
	        Dim field As New MergeField() With {.PropertyPath = "FirstName"}
	
	        '#End Region
	
	        '#Region "mode"
	
	        field.DisplayMode = FieldDisplayMode.Result
	
	        Me.radRichTextEditor1.Document.ChangeFieldDisplayMode(field.FieldStart, FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.ChangeFieldDisplayMode(field.FieldStart, FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.Document.ChangeAllFieldsDisplayMode(FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.ChangeAllFieldsDisplayMode(FieldDisplayMode.Result)
	
	        '#End Region
	
	        '#Region "insert"
	
	        Me.radRichTextEditor1.InsertField(field)
	
	        Me.radRichTextEditor1.InsertField(field, FieldDisplayMode.DisplayName)
	
	        '#End Region
	
	        '#Region "preview"
	
	        Me.radRichTextEditor1.PreviewFirstMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewLastMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewMailMergeDataRecordAtIndex(0)
	
	        Me.radRichTextEditor1.PreviewNextMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewPreviousMailMergeDataRecord()
	
	        '#End Region
	
	        Dim index As Integer = 0
	
	        '#Region "perform"
	
	        Me.radRichTextEditor1.MailMergeCurrentRecord() ' returns a RadDocument that is the result of substituting the merge fields with the data from the current record. The current record can be specified through the MailMergeSource API:</para>
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToFirst()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToLast()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToNext()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToPrevious()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToIndex(index)
	
	        Me.radRichTextEditor1.MailMerge(False) ' returns a RadDocument that is the result of Mail Merging all records. The parameter specifies if a page break should be inserted between the records (default value is true).
	
	        '#End Region
	    End Sub
	End Class
	
	#Region "data"
	
	Public Class ExamplesDataContext
	
	    Private _employees As New List(Of Employee)() From {
	        New Employee() With {.FirstName = "Andrew", .LastName = "Fuller", .JobTitle = "Director - Finance"},
	        New Employee() With {.FirstName = "Nancy", .LastName = "Davolio", .JobTitle = "Director - Human Resources"},
	        New Employee() With {.FirstName = "Robert", .LastName = "King", .JobTitle = "Engineering Design Manager"},
	        New Employee() With {.FirstName = "Margaret", .LastName = "Peacock", .JobTitle = "Finance & Investments Officer"}
	    }
	
	    Public ReadOnly Property Employees() As List(Of Employee)
	        Get
	            Return Me._employees
	        End Get
	    End Property
	End Class
	
	Public Class Employee
	    Public Property FirstName() As String
	
	    Public Property LastName() As String
	
	    Public Property JobTitle() As String
	End Class
	
	#End Region



This fields will look for the value of the FirstName property of the Employee objects.

### Changing the display mode of merge fields:

#### __[C#] __

{{region mode}}
	
	            field.DisplayMode = FieldDisplayMode.Result;
	
	            this.radRichTextEditor1.Document.ChangeFieldDisplayMode(field.FieldStart, FieldDisplayMode.Result);
	            
	            this.radRichTextEditor1.ChangeFieldDisplayMode(field.FieldStart, FieldDisplayMode.Result);
	            
	            this.radRichTextEditor1.Document.ChangeAllFieldsDisplayMode(FieldDisplayMode.Result);
	
	            this.radRichTextEditor1.ChangeAllFieldsDisplayMode(FieldDisplayMode.Result);
	            
	{{endregion}}



#### __[VB.NET] __

{{region mode}}
	
	        field.DisplayMode = FieldDisplayMode.Result
	
	        Me.radRichTextEditor1.Document.ChangeFieldDisplayMode(field.FieldStart, FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.ChangeFieldDisplayMode(field.FieldStart, FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.Document.ChangeAllFieldsDisplayMode(FieldDisplayMode.Result)
	
	        Me.radRichTextEditor1.ChangeAllFieldsDisplayMode(FieldDisplayMode.Result)
	
	        '#End Region
	
	        '#Region "insert"
	
	        Me.radRichTextEditor1.InsertField(field)
	
	        Me.radRichTextEditor1.InsertField(field, FieldDisplayMode.DisplayName)
	
	        '#End Region
	
	        '#Region "preview"
	
	        Me.radRichTextEditor1.PreviewFirstMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewLastMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewMailMergeDataRecordAtIndex(0)
	
	        Me.radRichTextEditor1.PreviewNextMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewPreviousMailMergeDataRecord()
	
	        '#End Region
	
	        Dim index As Integer = 0
	
	        '#Region "perform"
	
	        Me.radRichTextEditor1.MailMergeCurrentRecord() ' returns a RadDocument that is the result of substituting the merge fields with the data from the current record. The current record can be specified through the MailMergeSource API:</para>
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToFirst()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToLast()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToNext()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToPrevious()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToIndex(index)
	
	        Me.radRichTextEditor1.MailMerge(False) ' returns a RadDocument that is the result of Mail Merging all records. The parameter specifies if a page break should be inserted between the records (default value is true).
	
	        '#End Region
	    End Sub
	End Class
	
	#Region "data"
	
	Public Class ExamplesDataContext
	
	    Private _employees As New List(Of Employee)() From {
	        New Employee() With {.FirstName = "Andrew", .LastName = "Fuller", .JobTitle = "Director - Finance"},
	        New Employee() With {.FirstName = "Nancy", .LastName = "Davolio", .JobTitle = "Director - Human Resources"},
	        New Employee() With {.FirstName = "Robert", .LastName = "King", .JobTitle = "Engineering Design Manager"},
	        New Employee() With {.FirstName = "Margaret", .LastName = "Peacock", .JobTitle = "Finance & Investments Officer"}
	    }
	
	    Public ReadOnly Property Employees() As List(Of Employee)
	        Get
	            Return Me._employees
	        End Get
	    End Property
	End Class
	
	Public Class Employee
	    Public Property FirstName() As String
	
	    Public Property LastName() As String
	
	    Public Property JobTitle() As String
	End Class
	
	#End Region



### Inserting a MergeField at the current position of the caret:

#### __[C#] __

{{region insert}}
	
	            this.radRichTextEditor1.InsertField(field);
	
	            this.radRichTextEditor1.InsertField(field, FieldDisplayMode.DisplayName);
	
	{{endregion}}



#### __[VB.NET] __

{{region insert}}
	
	        Me.radRichTextEditor1.InsertField(field)
	
	        Me.radRichTextEditor1.InsertField(field, FieldDisplayMode.DisplayName)
	
	        '#End Region
	
	        '#Region "preview"
	
	        Me.radRichTextEditor1.PreviewFirstMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewLastMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewMailMergeDataRecordAtIndex(0)
	
	        Me.radRichTextEditor1.PreviewNextMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewPreviousMailMergeDataRecord()
	
	        '#End Region
	
	        Dim index As Integer = 0
	
	        '#Region "perform"
	
	        Me.radRichTextEditor1.MailMergeCurrentRecord() ' returns a RadDocument that is the result of substituting the merge fields with the data from the current record. The current record can be specified through the MailMergeSource API:</para>
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToFirst()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToLast()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToNext()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToPrevious()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToIndex(index)
	
	        Me.radRichTextEditor1.MailMerge(False) ' returns a RadDocument that is the result of Mail Merging all records. The parameter specifies if a page break should be inserted between the records (default value is true).
	
	        '#End Region
	    End Sub
	End Class
	
	#Region "data"
	
	Public Class ExamplesDataContext
	
	    Private _employees As New List(Of Employee)() From {
	        New Employee() With {.FirstName = "Andrew", .LastName = "Fuller", .JobTitle = "Director - Finance"},
	        New Employee() With {.FirstName = "Nancy", .LastName = "Davolio", .JobTitle = "Director - Human Resources"},
	        New Employee() With {.FirstName = "Robert", .LastName = "King", .JobTitle = "Engineering Design Manager"},
	        New Employee() With {.FirstName = "Margaret", .LastName = "Peacock", .JobTitle = "Finance & Investments Officer"}
	    }
	
	    Public ReadOnly Property Employees() As List(Of Employee)
	        Get
	            Return Me._employees
	        End Get
	    End Property
	End Class
	
	Public Class Employee
	    Public Property FirstName() As String
	
	    Public Property LastName() As String
	
	    Public Property JobTitle() As String
	End Class
	
	#End Region



### Previewing the results of Mail Merge:

#### __[C#] __

{{region preview}}
	            
	            this.radRichTextEditor1.PreviewFirstMailMergeDataRecord();
	            
	            this.radRichTextEditor1.PreviewLastMailMergeDataRecord();
	
	            this.radRichTextEditor1.PreviewMailMergeDataRecordAtIndex(0);
	
	            this.radRichTextEditor1.PreviewNextMailMergeDataRecord();
	
	            this.radRichTextEditor1.PreviewPreviousMailMergeDataRecord();
	
	{{endregion}}



#### __[VB.NET] __

{{region preview}}
	
	        Me.radRichTextEditor1.PreviewFirstMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewLastMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewMailMergeDataRecordAtIndex(0)
	
	        Me.radRichTextEditor1.PreviewNextMailMergeDataRecord()
	
	        Me.radRichTextEditor1.PreviewPreviousMailMergeDataRecord()
	
	        '#End Region
	
	        Dim index As Integer = 0
	
	        '#Region "perform"
	
	        Me.radRichTextEditor1.MailMergeCurrentRecord() ' returns a RadDocument that is the result of substituting the merge fields with the data from the current record. The current record can be specified through the MailMergeSource API:</para>
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToFirst()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToLast()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToNext()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToPrevious()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToIndex(index)
	
	        Me.radRichTextEditor1.MailMerge(False) ' returns a RadDocument that is the result of Mail Merging all records. The parameter specifies if a page break should be inserted between the records (default value is true).
	
	        '#End Region
	    End Sub
	End Class
	
	#Region "data"
	
	Public Class ExamplesDataContext
	
	    Private _employees As New List(Of Employee)() From {
	        New Employee() With {.FirstName = "Andrew", .LastName = "Fuller", .JobTitle = "Director - Finance"},
	        New Employee() With {.FirstName = "Nancy", .LastName = "Davolio", .JobTitle = "Director - Human Resources"},
	        New Employee() With {.FirstName = "Robert", .LastName = "King", .JobTitle = "Engineering Design Manager"},
	        New Employee() With {.FirstName = "Margaret", .LastName = "Peacock", .JobTitle = "Finance & Investments Officer"}
	    }
	
	    Public ReadOnly Property Employees() As List(Of Employee)
	        Get
	            Return Me._employees
	        End Get
	    End Property
	End Class
	
	Public Class Employee
	    Public Property FirstName() As String
	
	    Public Property LastName() As String
	
	    Public Property JobTitle() As String
	End Class
	
	#End Region



### Performing MailMerge:

#### __[C#] __

{{region perform}}
	            
	            this.radRichTextEditor1.MailMergeCurrentRecord(); // returns a RadDocument that is the result of substituting the merge fields with the data from the current record. The current record can be specified through the MailMergeSource API:</para>
	    
	            this.radRichTextEditor1.Document.MailMergeDataSource.MoveToFirst();
	    
	            this.radRichTextEditor1.Document.MailMergeDataSource.MoveToLast();
	    
	            this.radRichTextEditor1.Document.MailMergeDataSource.MoveToNext();
	        
	            this.radRichTextEditor1.Document.MailMergeDataSource.MoveToPrevious();
	            
	            this.radRichTextEditor1.Document.MailMergeDataSource.MoveToIndex(index);
	                
	            this.radRichTextEditor1.MailMerge(false); // returns a RadDocument that is the result of Mail Merging all records. The parameter specifies if a page break should be inserted between the records (default value is true).
	            
	{{endregion}}



#### __[VB.NET] __

{{region perform}}
	
	        Me.radRichTextEditor1.MailMergeCurrentRecord() ' returns a RadDocument that is the result of substituting the merge fields with the data from the current record. The current record can be specified through the MailMergeSource API:</para>
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToFirst()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToLast()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToNext()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToPrevious()
	
	        Me.radRichTextEditor1.Document.MailMergeDataSource.MoveToIndex(index)
	
	        Me.radRichTextEditor1.MailMerge(False) ' returns a RadDocument that is the result of Mail Merging all records. The parameter specifies if a page break should be inserted between the records (default value is true).
	
	        '#End Region
	    End Sub
	End Class
	
	#Region "data"
	
	Public Class ExamplesDataContext
	
	    Private _employees As New List(Of Employee)() From {
	        New Employee() With {.FirstName = "Andrew", .LastName = "Fuller", .JobTitle = "Director - Finance"},
	        New Employee() With {.FirstName = "Nancy", .LastName = "Davolio", .JobTitle = "Director - Human Resources"},
	        New Employee() With {.FirstName = "Robert", .LastName = "King", .JobTitle = "Engineering Design Manager"},
	        New Employee() With {.FirstName = "Margaret", .LastName = "Peacock", .JobTitle = "Finance & Investments Officer"}
	    }
	
	    Public ReadOnly Property Employees() As List(Of Employee)
	        Get
	            Return Me._employees
	        End Get
	    End Property
	End Class
	
	Public Class Employee
	    Public Property FirstName() As String
	
	    Public Property LastName() As String
	
	    Public Property JobTitle() As String
	End Class
	
	#End Region



You can further choose what you wish to do with the resulting RadDocument – assign it to a RadRichTextEditor’s Document property, export it, etc.