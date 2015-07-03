#Great way to get an intro to Razor and what you can access with it.

# Introduction #

take this Razor that you see and add it to a TBB. Then make a Component Template that uses it, and link that CT to all of your schemas in your dev environment. Now you have both a list of stuff you can access, and a way to see all of the stuff you need, for any given component.This uses `TridionObject`, which enables you to access all of the TOM.NET properties and methods that are available for the object.

See this for details: http://blog.frankmtaylor.com/2013/05/14/make-a-debugging-tbb-for-tridion-2011-using-razor-mediator/
# The Code #
---
```
@using System.IO
 
<style type="text/css">
table{color: #333; text-align: left; min-width: 400px; border-collapse: collapse; border:1px solid gray;}
th, td {padding: .618em} 
thead th, thead td { font-size: 1.15em; border-bottom: 2px solid #494949; background: #f1f1f1}
tbody th, tbody td {border-bottom:1px solid #555}
tbody td:nth-child(2){}
caption{font-size: .95em}
.compInfo {color: #333}
h1, h2, h3 {border-bottom: 1px solid #456}
details, summary {outline:none}
details {font-size: .75em; paddingborder: 2px solid #f1f1f1; background: #fdfdfd}
summary {font-size: 1.25em; padding: .618em; background: #f1f1f1; border-bottom: 1px solid #456}
summary > * {display:inline-block; margin:0; border:none}
details summary ~ *{margin-left: 1em }
</style>
<div class="compInfo">
	<h1>Title: 
	@Component.Title
	</h1>
	<details>
		<summary>
			<h3>Fields and Values</h3>
		</summary>
		<table>
			<thead>
				<tr>
					<th>Field</th>
					<th>Value</th>
				</tr>
			</thead>
			<tbody>
		@foreach (var field in @Fields.GetFields()) {
		    	<tr>
		    		<th>@field.Key</th>
		    		<td>@field.Value</td>
		    	</tr>
		}
			</tbody>
		</table>
	</details>
	<details>
		<summary>
			<h3>ComponentType: @Component.TridionObject.ComponentType</h3>
		</summary>
		@if(Component.TridionObject.ComponentType.ToString() =="Multimedia"){
			<table>
				<tr>
					<th>
						FileName
					</th>
					<td>
						@Component.TridionObject.BinaryContent.Filename
					</td>
				</tr>
				<tr>
					<th>
						Filesize
					</th>
					<td>
						@Component.TridionObject.BinaryContent.FileSize
					</td>
				</tr>
				<tr>
					<th>
						Is external
					</th>
					<td>
						@Component.TridionObject.BinaryContent.IsExternal
					</td>
				</tr>
				<tr>
					<th>
						MultimediaType
					</th>
					<td>
						@Component.TridionObject.BinaryContent.MultimediaType
						<br />
 
					</td>
				</tr>
				<tr>
					<th>
						UploadFromFile
					</th>
					<td>
						@Component.TridionObject.BinaryContent.UploadFromFile
					</td>
				</tr>
				<tr>
					<th>
						UploadFromStream
					</th>
					<td>
						@Component.TridionObject.BinaryContent.UploadFromStream
					</td>
				</tr>
			</table>
		}
	</details>
	<details>
		<summary>
			<h3>Schema: @Component.Schema</h3>
		</summary>
	<table>
		<caption>Schema information</caption>
		<tr>
			<th>
				Title
			</th>
			<td>
				@Component.TridionObject.Schema.Title
			</td>
		</tr>
		<tr>
			<th>
				Purpose
			</th>
			<td>
				@Component.TridionObject.Schema.Purpose
			</td>
		</tr>
		<tr>
			<th>
				root element
			</th>
			<td>
				@Component.TridionObject.Schema.RootElementName
			</td>
		</tr>
	</table>
</details>
	<details>
		<summary>
			<h3>Metadata: @(Component.Metadata != null ? "has metadata" : "no metadata ")</h3>
		</summary>
		<h4>metadata schema: 
		@Component.MetadataSchema
		</h4>
		<table>
			<caption>Metadata Fields and Content</caption>
			<thead>
				<tr>
					<th>Field</th>
					<th>Value</th>
				</tr>
			</thead>
			<tbody>
		@foreach (var field in @Component.Metadata.GetFields()) {
		    	<tr>
		    		<th>@field.Key</th>
		    		<td>@field.Value</td>
		    	</tr>
		}
			</tbody>
		</table>
	</details>
	<details>
		<summary>
			<h3>Version and Revision Info</h3>
		</summary>
		<table>
			<tr>
				<th>
					Version
				</th>
				<td>
					@Component.TridionObject.Version
				</td>
			</tr>
			<tr>
				<th>
					Revision Date
				</th>
				<td>
					@Component.TridionObject.RevisionDate
				</td>
			</tr>
			<tr>
				<th>
					Revision
				</th>
				<td>
					@Component.TridionObject.Revision
				</td>
			</tr>	
		</table>
		<table>
			<tr>
				<th>Revisor</th>
				<td>
					@Component.TridionObject.Revisor
				</td>
			<tr>
				<th>description</th>
				<td>
					@Component.TridionObject.Revisor.Description
				</td>
			<tr>
				<th>title</th>
				<td>@Component.TridionObject.Revisor.Title
				</td>
			<tr>
				<th>is admin</th>
				<td>
					@Component.TridionObject.Revisor.IsSystemAdministrator
				</td>
		</table>
	</details>
 
	<h3>WebDav Url: 
	@Component.WebDavUrl
	</h3>
	<h3>path: 
	@Component.Path
	</h3>
	<h3>Session: 
	@Component.TridionObject.Session
	</h3>
	<details>
		<summary>
			<h3>Owning repository: 
			@Component.TridionObject.OwningRepository
			</h3>
		</summary>
		<table>
			<tr>
				<th>
					Title
				</th>
				<td>
					@Component.TridionObject.OwningRepository.Title
				</td>
			</tr>
			<tr>
				<th>
					Publication Key
				</th>
				<td>
					@Component.TridionObject.OwningRepository.Key
				</td>
			</tr>
			<tr>
			<tr>
				<th>
					Multimedia Path
				</th>
				<td>
					@Component.TridionObject.OwningRepository.MultimediaPath
				</td>
			</tr>
			<tr>
				<th>
					Multimedia URL
				</th>
				<td>
					@Component.TridionObject.OwningRepository.MultimediaUrl
				</td>
			</tr>
			<tr>
				<th>
					HasChildren
				</th>
				<td>
					@Component.TridionObject.OwningRepository.HasChildren
				</td>
			</tr>
			<tr>
				<th>
					RootFolder
				</th>
				<td>
					@Component.TridionObject.OwningRepository.RootFolder
					<br />
					( @Component.TridionObject.OwningRepository.RootFolder.Title	)				
				</td>
			</tr>
			<tr>
				<th>
					RootStructureGroup
				</th>
				<td>
					@Component.TridionObject.OwningRepository.RootStructureGroup
					<br />
					( @Component.TridionObject.OwningRepository.RootStructureGroup.Title )
				</td>
			</tr>
 
		</table>
	</details>
	<h3>Organization item: 
	@Component.TridionObject.OrganizationalItem
	</h3>
 
	<h3>LockType: 
	@Component.TridionObject.LockType
	</h3>
	<h3>LoadState: 
	@Component.TridionObject.LoadState
	</h3>
	<h3>IsShared: 
	@Component.IsShared
	</h3>
	<h3>IsPublishedInContext: 
	@Component.TridionObject.IsPublishedInContext
	</h3>
	<h3>IsLocalized: 
	@Component.IsLocalized
	</h3>
	<h3>Allowed Actions: 
	@Component.TridionObject.AllowedActions
	</h3>
	<h3>ApprovalStatus: 
	@Component.TridionObject.ApprovalStatus
	</h3>
</div>
<details>
	<summary>
		<h3>Keywords</h3>
	</summary>
	<table>
	@foreach (var keyword in Component.TridionObject.GetUsedKeywords()){
		<tr>
			<td>@keyword.Id</td>
			<td> @keyword.Title</td>
		</tr>
	}
	</table>
</details>
<details>
	<summary>
		<h3>Items this uses</h3>
	</summary>
	<table>
	@foreach(var usedItem in Component.TridionObject.GetUsedItems()){
		<tr>
			<td>@usedItem.Id</td>
			<td> @usedItem.Title</td>
		</tr>
	}
	</table>
</details>
<details>
	<summary>
		<h3>Items this is used in</h3>
	</summary>
	<table>
	@foreach(var usedItem in Component.TridionObject.GetUsingItems()){
		<tr>
			<td>@usedItem.Id</td>
			<td> @usedItem.Title</td>
		</tr>
	}
	</table>
</details>
```