Generador automatizado de Stored Procedure para CRUD para SQL basado en tablas existentes
<article class="markdown-body entry-content container-lg" itemprop="text"><h1 dir="auto"><a id="user-content-sp_crudgen" class="anchor" aria-hidden="true" href="#sp_crudgen"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>sp_CRUDGenerate_SQL</h1>
<p dir="auto">sp_CRUDGenerate_SQL is a free open-source SQL Server stored procedure that generates stored procedures for you based on your tables and metadata like foreign keys and data types. The generated stored procedure code utilizes the SQL Server community best practices.</p>
<p dir="auto">You can use sp_CRUDGenerate_SQL to generate 11 different stored procedures from basic your <strong>C</strong>reate, <strong>R</strong>ead, <strong>U</strong>pdate, <strong>D</strong>elete, <strong>U</strong>psert stored procedures to extremely advanced safe dynamic <strong>S</strong>earch stored procedures otherwise known as optional parameters, kitchen sink, Swiss army knife, catch-all queries.</p>
<p dir="auto">sp_CRUDGenerate_SQL will auto-generate and regenerate stored procedures for you. If you want to customize one of the generated stored procedures you can remove <code>&lt;auto-generated&gt;</code> comment section and the stored procedure will not be overwritten.</p>
<p dir="auto">Install and execute sp_CRUDGenerate_SQL in the user database and not master.</p>
<p dir="auto">The runtime depends on the complexity of your table structure.</p>
<p dir="auto">Fork the repo to change the T-SQL style (or format with a tool like Redgate SQL Prompt) and naming conventions. Remember to create a pull request if you added something cool so the rest of the community can benefit.</p>
<p dir="auto">Table names should be PascalCase for best table alias naming.</p>
<p dir="auto">Use FOREIGN KEY REFERENCES between tables for ReadEager and Search to recurse over related tables.</p>
<p dir="auto">There are paramaters you can set in sp_CRUDGenerate_SQL to customize for your column naming convention and stored procedure generations.</p>
<table>
<thead>
<tr>
<th>Parameter Name</th>
<th>Description</th>
<th>Default</th>
</tr>
</thead>
<tbody>
<tr>
<td>@GenerateStoredProcedures</td>
<td>0 = Will only create the generated T-SQL to create the stored procedures, 1 = Will also create the stored procedures</td>
<td>0</td>
</tr>
<tr>
<td>@SchemaTableOrViewName</td>
<td>NULL = Generate all tables &amp; views, [SCHEMA.TABLEORVIEWNAME] or [TABLEORVIEWNAME] for just one table or view. <strong>NOTE:</strong> The leading column on the view should be the lowest grain primary key of the results. If there will be multiple contacts from a company returned in the results, ContactId should be the leading key on the view. If the view will only contain results for companies, then the leading column on the view should be CompanyId.</td>
<td>NULL</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>@GenerateCreate</td>
<td>1 = Generate the Create stored procedure, 0 = Will not generate the Create stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateCreateMultiple</td>
<td>1 = Generate the Create stored procedure, 0 = Will not generate the Create stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateRead</td>
<td>1 = Generate the Read stored procedure, 0 = Will not generate the Read stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateReadEager</td>
<td>1 = Generate the ReadEager stored procedure, 0 = Will not generate the ReadEager stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateUpdate</td>
<td>1 = Generate the Update stored procedure, 0 = Will not generate the Update stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateUpdateMultiple</td>
<td>1 = Generate the Update stored procedure, 0 = Will not generate the Update stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateUpsert</td>
<td>1 = Generate the Upsert stored procedure, 0 = Will not generate the Upsert stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateIndate</td>
<td>1 = Generate the Indate stored procedure, 0 = Will not generate the Indate stored procedure</td>
<td>0</td>
</tr>
<tr>
<td>@GenerateDelete</td>
<td>1 = Generate the Delete stored procedure, 0 = Will not generate the Delete stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateDeleteMultiple</td>
<td>1 = Generate the DeleteMultiple stored procedure, 0 = Will not generate the DeleteMultiple stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@GenerateSearch</td>
<td>1 = Generate the Search stored procedure, 0 = Will not generate the Search stored procedure</td>
<td>1</td>
</tr>
<tr>
<td>@SearchSeparatorString</td>
<td>Set this string to match your separator used when passing in a search parameter using the 'Between', 'BetweenWithBlanks', 'NotBetween', and 'NotBetweenWithBlanks' operators</td>
<td>' to '</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>@RowCreatePersonColumnName</td>
<td>Is the column name used in your tables for the person who created a row. FOREIGN KEY REFERENCES to a Person table.</td>
<td>RowCreatePersonId</td>
</tr>
<tr>
<td>@RowCreatePersonInclude</td>
<td>1 = Will generate table joins to the person table, 0 = Will not generate table joins to the person table</td>
<td>0</td>
</tr>
<tr>
<td>@RowCreateTimeColumnName</td>
<td>Is the column name used in your tables to capture the datetime when the row was created.</td>
<td>RowCreateTime</td>
</tr>
<tr>
<td>@RowCreateTimeFunction</td>
<td>Is the system date function you want used in your tables for the @RowCreateTimeColumnName to capture when the row was created. {SYSDATETIMEOFFSET(), SYSUTCDATETIME(), SYSDATETIME(), GETUTCDATE(), GETDATE(), CURRENT_TIMESTAMP}</td>
<td>SYSDATETIMEOFFSET()</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>@RowUpdatePersonColumnName</td>
<td>Is the column name used in your tables for the person who updated a row. FOREIGN KEY REFERENCES to a Person table.</td>
<td>RowUpdatePersonId</td>
</tr>
<tr>
<td>@RowUpdatePersonInclude</td>
<td>1 = Will generate table joins to the person table, 0 = Will not generate table joins to the person table</td>
<td>0</td>
</tr>
<tr>
<td>@RowUpdateTimeColumnName</td>
<td>Is the column name used in your tables to capture the datetime when the row was last updated.</td>
<td>RowUpdateTime</td>
</tr>
<tr>
<td>@RowUpdateTimeFunction</td>
<td>Is the system date function you want used in your tables for the @RowUpdateTimeColumnName to capture when the row was updated.  {SYSDATETIMEOFFSET(), SYSUTCDATETIME(), SYSDATETIME(), GETUTCDATE(), GETDATE(), CURRENT_TIMESTAMP}</td>
<td>SYSDATETIMEOFFSET()</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>@RowVersionStampColumnName</td>
<td>Is the column name in your tables for the rowversion/timestamp used for optimistic concurrency in the delete and update stored procedures.</td>
<td>RowVersionStamp</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>@TemporalRowStartColumName</td>
<td>Is the system-versioned temporal tables column name in your tables for the start period (GENERATED ALWAYS AS ROW START). This column will be ignored for inserts and deletes.</td>
<td>RowValidFromTime</td>
</tr>
<tr>
<td>@TemporalRowEndColumName</td>
<td>Is the system-versioned temporal tables column name in your tables for the end period (GENERATED ALWAYS AS ROW END). This column will be ignored for inserts and deletes.</td>
<td>RowValidToTime</td>
</tr>
<tr>
<td>@ForceTemporalForView</td>
<td>1 = Forces the view to allow temporal functionality, 0 = The view will not allow temporal functionality</td>
<td>0</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>@VersionCheckMode</td>
<td>1 = Will only return the version number and not execute, 0 = Will execute this stored procedure</td>
<td>0</td>
</tr>
</tbody>
</table>
<p dir="auto">The Search stored procedure does not work with every column data type.</p>
<p dir="auto">If you use extended properties description names on tables and columns they will be included as comments in the stored procedures.</p>
<p dir="auto">Do not use SQL Server reserved keywords in object names.</p>
<p dir="auto">Runs on SQL Server 2016, 2017, 2019, Azure SQL Server. JSON support can be changed to XML for 2014 and lower.</p>
</article>
