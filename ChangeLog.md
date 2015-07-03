# Version 1.3.3 #
  * Fixes memory leak issue that some people were facing.
  * Removes the expiring cache feature which is no longer needed.
  * Fixes issue with relative @importRazor() statements not getting added as a Where Used reference.
  * Better performance.

# Version 1.3.2 #
  * Fixed Installer so that it installs with Tridion 2013.
  * Updated the Template property for ComponentPresentationModels so that they return a ComponentTemplateModel rather than ComponentTemplate.
  * Added a Version property to the template base to easily check the current Razor version via @Version.
  * Added a GetComponentTemplate() method to the ModelUtilities class.

# Version 1.3.1 #
  * Added ability to get from index for DynamicPackage and DynamicItemFields. ie: @Fields["FieldName"], @Package["someKey"]. For Package, allows for retrieving values with dots in them.
  * Added Dominic Cronin's patch for DynamicPatch to not cache package items as they can change.
  * FIXES for issues with 1.3 regarding creating new TBBs/imports when imports were included from config.
  * Added ParentKeywords and RelatedKeywords properties to KeywordModel.
  * 1.3.1 documentation and forward using Robert Curlette's updated 1.3 documentation removing smart quotes.
  * Added fix to IsSiteEditEnabled... would throw error if a Publication Target was never enabled/disabled with SiteEdit before.
  * Added GetFieldNames() and GetFields() to DynamicItemFields to support generic templates.

# Version 1.3 #
  * Fixed DynamicPackage for ComponentArray items (before would always return an empty list of ComponentModels).
  * IsSiteEditEnabled property - Check to see if site edit is enabled or not.
  * Modified RenderComponentField methods to not throw exception. Outputs empty tcdl tags (or an empty string with correct parameter).
  * Fix for IsLast property on ComponentPresentationModel when retrieved via the GetComponentPresentationsBy... methods.
  * Added functionality for import statements to accept relative webdav URLs. ie: importRazor("../test.cshtml") importRazor("Directory/Template.cshtml")
  * Fix for reading local version of razor templates when imported in child publication.
  * Added Where Used functionality for imported TBBs.
  * Added configurative settings to control Where Used functionality, and ability to replace relative paths with full paths if desired.
  * Added MetadataSchema property to PublicationModel and AbstractRepositoryLocalObject.
  * Prior Metadata code only checked if metadata schema existed.  If schema was added after components were created, and those components weren't updated, they would get an error.  Updated check to check both xml content and schema.
  * Modified @Metadata to work on both Page and Component templates.  If its a page template, will access the Page's metadata fields.  If component template, will access the Component's metadata fields.
  * Added PageTemplateModel, ComponentTemplateModel, and RazorTemplateModel.  Accessible from base template as @PageTemplate (Accessible as long as a Page can be found, from either CT or PT), @ComponentTemplate (accessible only if its a Component Template), and RazorTemplate (the razor TBB itself).  These classes have access to normal properties such as Metadata.
  * Added more lines to the output of CompilerErrors for better debugging of compile time errors.

# Version 1.2 #

  * Updated GetComponentPresentationsByTemplate(string templateName) to GetComponentPresentationsByTemplate(params string[.md](.md) templateNames).  Allows the method to take multiple values.
  * Updated GetComponentPresentationsBySchema(string schemaName) to GetComponentPresentationsBySchema(params string[.md](.md) schemaNames). Allows the method to take multiple values.
  * Added RenderComponentPresentations() - returns a string of all rendered component presentations on page.
  * Added RenderComponentPresentationsByTemplate(params string[.md](.md) templateNames) - returns a string of all rendered component presentations given the passed template names.
  * Fix - Existing cache issue made it so that if a template failed to compile (compile exception), until that template was fixed or until the cache expired, anyone else attempting to save a template would get the same error message.
  * Updated the compile errors that are output.  Now gives the line of code giving the error.  Note that this is the generated code line of error and not your exact razor line of error.  For example, "<div>@YourClass.Blah</div>" could show the line as being "Write(YourClass.Blah);".
  * Added Helper/Custom Function Import. Add global helper/custom functions to your templates, either globally via configuration or directly from your Razor templates.  Helper/custom functions can be stored either as a Razor Template Building Block, or as an external text file on the CMS server.
  * Added Index to ComponentPresentationModel. Calling @ComponentPresentations, or any of the GetComponentPresentationsBy... methods will auto generate the Index property of the ComponentPresentationModels in the list to be consumed by your templates.
  * Added IsFirst and IsLast property to ComponentPresentationModel.  Like Index, these are only set when retreiving via ComponentPresentations property or via the GetComponentPresentationsBy... methods.
  * Added Index, IsFirst, and IsLast properties to DynamicItemFields. Auto set when a field type is a multivalued EmbeddedField.
  * Added Index, IsFirst, and IsLast properties to KeywordModel and ComponentModel as well.  Auto set when a field type is a multivalued KeywordField or multivalued ComponentLinkField.
  * Added logging methods directly to the template base class.  Prior to this release, the documentation was wrong regarding @Log.Debug("Your message")... that syntax would actually throw an error.  The correct way was @{ Log.Debug("Your message"); }.  You can now call @Debug("..."), @Error("..."), @Info("...") and @Warning("...") right from your templates!
  * Added property StructureGroupAncestry to PageMode instances.  Contains a list of StructureGroups from the root to the page's StructureGroup.
  * Fix to allow webdav URLs to be picked up in the extract binaries process of the Razor Mediator.
  * Update to ComponentModel for Multimedia Components only, so that both Fields and Metadata will point to the Metadata fields.
  * Fix to make the cached compiled templates to be thread safe.

# Version 1.0.1 / 1.1 #

  * Fix for the DynamicItemFields class.  Wasn't properly handling empty values for certain fields (like ComponentFields and EmbeddedSchemaFields).
  * Fix for "HasValue(string)" method.
  * Updated so that Component and Page gets via package name "Component" and "Page" rather than types.
  * Added KeywordModel for Tridion Keywords (easily get Metadata fields now just like other DynamicItemFields)
  * Fix for adding assemblies to your templates
  * Fix for loading assemblies via GAC (and updated sample in installed config)
  * Fix for installer. Uninstall was not removing the Mediator section.
  * Added utility function to template base, GetComponentPresentationsBySchema(schemaName)
  * Fixed Dynamic Package.  @Package was actually set to the Tridion Package instance.  Now set to the DynamicPackage instance so you can call @Package.packageItemName.  Also added the GetByName(), GetByType(), and GetValue() methods to the DynamicPackage class.