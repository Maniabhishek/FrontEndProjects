## GSoft.Dynamite ##

# T:GSoft.Dynamite.Binding.EntityPropertyConversionDetail

 Details for an entity binding. 



---
##### M:GSoft.Dynamite.Binding.EntityPropertyConversionDetail.#ctor(System.Reflection.PropertyInfo,System.String,GSoft.Dynamite.Binding.BindingType,GSoft.Dynamite.ValueTypes.Writers.IBaseValueWriter,GSoft.Dynamite.ValueTypes.Readers.IBaseValueReader)

 Initializes a new instance of the [[|!:EntityBindingDetail]] class. 

|Name | Description |
|-----|------|
|entityProperty: |The entity property.|
|Name | Description |
|-----|------|
|valueKey: |The value key.|
|Name | Description |
|-----|------|
|bindingType: |Type of the binding.|
|Name | Description |
|-----|------|
|valueWriter: |Value writer for the associated value type|
|Name | Description |
|-----|------|
|valueReader: |Value reader for the associated value type|


---
##### P:GSoft.Dynamite.Binding.EntityPropertyConversionDetail.EntityProperty

 Gets or sets the entity property. 



---
##### P:GSoft.Dynamite.Binding.EntityPropertyConversionDetail.ValueKey

 Gets or sets the value key. 



---
##### P:GSoft.Dynamite.Binding.EntityPropertyConversionDetail.BindingType

 Gets the type of the binding. 



---
##### P:GSoft.Dynamite.Binding.EntityPropertyConversionDetail.ValueWriter

 Gets the writer instance that knows how to write the property's value type to SharePoint elements 



---
##### P:GSoft.Dynamite.Binding.EntityPropertyConversionDetail.ValueReader

 Gets the re instance that knows how to write the property's value type to SharePoint elements 



---
# T:GSoft.Dynamite.Binding.EntityBindingSchema

 A schema to apply on entities. 



---
# T:GSoft.Dynamite.Binding.IEntityBindingSchema

 A schema to apply on entities. 



---
##### P:GSoft.Dynamite.Binding.IEntityBindingSchema.EntityType

 The entity type described by the schema 



---
##### P:GSoft.Dynamite.Binding.IEntityBindingSchema.PropertyConversionDetails

 The mapping details for each property of the entity 



---
##### M:GSoft.Dynamite.Binding.EntityBindingSchema.#ctor(System.Type)

 Creates a new [[|T:GSoft.Dynamite.Binding.EntityBindingSchema]]

|Name | Description |
|-----|------|
|entityType: |The entity type described by the schema|


---
##### P:GSoft.Dynamite.Binding.EntityBindingSchema.EntityType

 The entity type described by the schema 



---
##### P:GSoft.Dynamite.Binding.EntityBindingSchema.PropertyConversionDetails

 The mapping details for each property of the entity 



---
# T:GSoft.Dynamite.Binding.CachedEntitySchemaFactory

 Decorator for [[|T:GSoft.Dynamite.Binding.EntitySchemaFactory]] which takes care of caching entity mapping details for all types. 



---
# T:GSoft.Dynamite.Binding.IEntitySchemaFactory

 Builds the schema of entity mapping details for all of an entity's properties tagged with the PropertyAttribute. 


