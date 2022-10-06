<!-- loioc0f6592a592e47f9bb6d09900de47412 -->

# Tables

 SAP Fiori elements supports several table types.

You can use the following table types:

-   Responsive tables

    Responsiveness is optimized for mobile use. Line items can be viewed with no scrolling or with only vertical scrolling, regardless of the display width.

    > ### Note:  
    > On mobile devices, a responsive table is used by default.
    > 
    > When launched on a mobile device, the responsive table automatically displays a button that allows users to expand to full-screen mode.
    > 
    > In SAP Fiori elements for OData V2 applications, this feature is available as of SAPUI5 1.96.
    > 
    > In SAP Fiori elements for OData V4 applications, this feature is available as of SAPUI5 1.98.

-   Grid table

    Desktop-centric table type that allows users to scroll in both directions. This table type can handle a large number of items and columns.

-   Analytical table

    Contains data structured in rows and columns. It provides several powerful options for working with data, including advanced grouping and aggregations.

    In contrast to other tables, the analytical data binding used by the analytical table automatically displays an aggregated number in a cell.

    > ### Note:  
    > On mobile devices, a responsive table is used instead of an analytical table – even if this was specified at application level.




The application decides which table representation is most suitable based on usage. The table toolbar is responsive. For information about available table types, see also [Tables: Which One Should I Choose?](../10_More_About_Controls/tables-which-one-should-i-choose-148892f.md).

For more information about defining the `UI.LineItem` annotation that describes the table, see [Defining Line Items](defining-line-items-f0e1e17.md).

The table control uses page mechanisms while loading data.

It contains the following:

-   Layout management
-   Toolbar with actions rendered as text icons, for example, *Personalize*

-   Application-specific actions rendered as text buttons, for example *Copy*, *Approve*, and *Delete*

-   Indication of draft status \(only for list report tables\)

-   Displays items locked by other users \(only for list report tables\)




### Default Selection Mode for Rows in Tables

By default, the table generated by the template is single-selection. Users select an item from the table to trigger a custom action, for example *Validate*, which then returns the results for the selected item. Applications can change this to multi-selection mode.

For more information, see [Enabling Multiple Selection in Tables](enabling-multiple-selection-in-tables-116b5d8.md).



<a name="loioc0f6592a592e47f9bb6d09900de47412__section_kgk_phh_wpb"/>

## Show/Hide Columns Based on Importance and Available Screen Size

You can show or hide columns of list report and object page tables depending on the screen width, for example if the browser window is small, if the app is running on a device with a smaller screen, or if you're using the flexible column layout. The value of the `UI.Importance` annotation for the field determines which columns are hidden or moved when the screen size is reduced.

You can use the `UI.Importance` annotation to set the importance for table columns as follows:

-   `High`: Columns are always visible on all screen sizes. When the screen size is reduced, the columns move to a pop-in area but remain visible.

-   `Low`: When the screen size is reduced, the columns with this importance setting are the first ones to move to a pop-in area and are hidden automatically.

-   `None` \(default\) and `Medium`: When the screen size is reduced, the columns with these importance settings are hidden automatically \(columns with the importance setting `Low` are considered first, as mentioned in the previous point\).


> ### Note:  
> Columns that have no importance setting \(`None`\) but contain a semantic key, are treated as `High` \(also when used in a `FieldGroup`\).

As soon as the first column is hidden, the *Show Details* button appears in the table toolbar. When a user clicks this button, the button text changes to *Hide Details* and all previously visible column information is shown as popins. If a user clicks the button again, the text changes back to *Show Details* and columns in popins are hidden again, except those for which the `UI.Importance` annotation is set to `High`.

> ### Sample Code:  
> XML annotation
> 
> ```xml
> <Annotations Target="STTA_PROD_MAN.STTA_C_MP_ProductSalesPriceType">
>      <Annotation Term="UI.LineItem">
>           <Collection>
>                <Record Type="UI.DataField">
>                     <PropertyValue Property="Value" Path="PriceDay" />
>                     <Annotation Term="UI.Importance" EnumMember="UI.ImportanceType/High" />
>                </Record>
>                <Record Type="UI.DataField">
>                      <PropertyValue Property="Value" Path="TargetPrice" />
>                      <!--This will be treated with default importance "None" which is same as "Medium"-->
>                </Record>
>                <Record Type="UI.DataField">
>                      <PropertyValue Property="Value" Path="DiscountPriceTarget" />
>                      <Annotation Term="UI.Importance" EnumMember="UI.ImportanceType/Low" />
>                </Record>
>           </Collection>
>      </Annotation>
> </Annotations>
> ```

> ### Note:  
> Since release SAPUI5 1.87, SAP Fiori elements automatically calculates the default column width and provides an option to resize the column width in responsive tables. This is the default behavior. Having fewer columns in a table increases the free space available on the right side of the table.



<a name="loioc0f6592a592e47f9bb6d09900de47412__section_u3p_z5q_sqb"/>

## Searching for Rows in a Table on an Object Page

In responsive, grid, and analytical tables, if the table is searchable \(that is, if an entity set is used for which `sap:searchable` is `true`\), a search field is displayed. You can search for particular rows in the table.



<a name="loioc0f6592a592e47f9bb6d09900de47412__section_uzk_54j_x4b"/>

## Define Column Width Using an Annotation

You can customize the width of a column defined in a line item using the UI annotation `com.sap.vocabularies.HTML5.v1.CssDefaults`. For more information, see [Setting the Default Column Width](setting-the-default-column-width-a765253.md).



<a name="loioc0f6592a592e47f9bb6d09900de47412__section_amq_ynw_xmb"/>

## Additional Features in SAP Fiori Elements for OData V2

The Tree table type is supported. It supports hierarchically structured data.



### Smart Multi-Input Control

[Smart multi-input](../10_More_About_Controls/smart-multi-input-5644169.md) is automatically rendered as a column in responsive and grid tables if a 1:N relationship exists in the association for the given column.

To configure smart multi-input fields on an object page, see [Using the Multi-Input Field on the Object Page](using-the-multi-input-field-on-the-object-page-04ff5b1.md).



### Vertical Alignment of Responsive Tables

You can set the vertical alignment property for a responsive table viathe `tableColumnVerticalAlignment` manifest property under the settings of `sap.ui.generic.app`, to the values `Top`, `Middle`, or `Bottom`.



<a name="loioc0f6592a592e47f9bb6d09900de47412__section_ey5_lvv_gnb"/>

## Additional Features in SAP Fiori Elements for OData V4

A responsive table is used by default. You can change this in the `manifest.json`.

Analytical tables are currently not supported on draft-enabled entities.



### Exclude Fields from Table Personalization

You can exclude specific fields from the table personalization dialog in the list report and object page. You can set the `availability` property of the column to `hidden`.

For more information, see the *availability* property in the *Settings* table in the topic [Example: Adding Columns to a Responsive Table in the List Report](example-adding-columns-to-a-responsive-table-in-the-list-report-28e9570.md).



### Handling of Search Restrictions

The search restriction for a table is first looked up in the parent entity \(via `NavigationRestrictions` at the parent entity, with the `NavigationProperty` pointing to the association of the table entity\).

-   Navigation Restrictions at Parent Entity

    > ### Sample Code:  
    > XML Annotation \(non-containment scenario\): /SalesOrderManage/\_Items
    > 
    > ```xml
    > <Annotations Target="com.c_salesordermanage_sd.Container/SalesOrderManage">
    >    <Annotation Term="Capabilities.NavigationRestrictions">
    >       <Record>
    >          <PropertyValue Property="RestrictedProperties">
    >             <Collection>
    >                <Record>
    >                   <PropertyValue Property="NavigationProperty" NavigationPropertyPath="_Items" />
    >                   <PropertyValue Property="SearchRestrictions">
    >                      <Record>
    >                         <PropertyValue Property="Searchable" Bool="false" />
    >                      </Record>
    >                   </PropertyValue>
    >                </Record>
    >             </Collection>
    >          </PropertyValue>
    >       </Record>
    >    </Annotation>
    > </Annotations>
    > ```

    > ### Sample Code:  
    > ABAP CDS Annotation
    > 
    > No ABAP CDS annotation sample is available. Please use the local XML annotation.

    > ### Sample Code:  
    > CAP CDS Annotation \(non-containment scenario\)
    > 
    > ```
    > entity SalesOrderManage @(
    >    Capabilities:{
    >       NavigationRestrictions:{
    >          RestrictedProperties:[{
    >             NavigationProperty : _Items,
    >             SearchRestrictions : {Searchable : false}
    >          }]
    >       }
    >    }
    > )
    > ```

    In a containment scenario \(for example, where the main entity set is from a parameterized entity\), you can maintain the annotations as shown in the following sample code:

    > ### Sample Code:  
    > XML Annotation \(containment scenario\): /Customer/Set/\_PartnerItems
    > 
    > ```xml
    > <Annotations Target="sap.fe.test.MyService.EntityContainer/Customer">
    >    <Annotation Term="Capabilities.NavigationRestrictions">
    >       <Record>
    >          <PropertyValue Property="RestrictedProperties">
    >             <Collection>
    >                <Record>
    >                   <PropertyValue Property="NavigationProperty" NavigationPropertyPath="Set/_PartnerItems" />
    >                   <PropertyValue Property="SearchRestrictions">
    >                      <Record>
    >                         <PropertyValue Property="Searchable" Bool="false" />
    >                      </Record>
    >                   </PropertyValue>
    >                </Record>
    >             </Collection>
    >          </PropertyValue>
    >       </Record>
    >    </Annotation>
    > </Annotations>
    > ```

    > ### Sample Code:  
    > ABAP CDS Annotation
    > 
    > No ABAP CDS annotation sample is available. Please use the local XML annotation.

    > ### Sample Code:  
    > CAP CDS Annotation \(containment scenario\)
    > 
    > ```
    > service MyService {
    >     @Capabilities.NavigationRestrictions.RestrictedProperties : [{
    >         $Type              : 'Capabilities.NavigationPropertyRestriction',
    >         NavigationProperty : 'Set/_PartnerItems',
    >         SearchRestrictions : {Searchable : false}
    >     }]
    > }
    > ```

-   Restrictions Directly at Child Entity

    If there is no search restriction defined at parent entity via the NavigationRestriction, then the search restriction defined directly on the table entity set \(child entity\) is considered.

    > ### Sample Code:  
    > XML Annotation \(non-containment scenario\): /SalesOrderManage/\_Items
    > 
    > ```xml
    > <Annotations Target="com.c_salesordermanage_sd.Container/SalesOrderItem">
    >    <Annotation Term="SAP__capabilities.SearchRestrictions">
    >       <Record>
    >          <PropertyValue Property="Searchable" Bool="false" />
    >       </Record>
    >    </Annotation>
    > </Annotations>
    > ```

    > ### Sample Code:  
    > ABAP CDS Annotation
    > 
    > No ABAP CDS annotation sample is available. Please use the local XML annotation.

    > ### Sample Code:  
    > CAP CDS Annotation \(non-containment scenario\)
    > 
    > ```
    > entity SalesOrderItem @(
    >    Capabilities:{
    >       SearchRestrictions : {Searchable : false}
    >    }
    > )
    > ```

    In a containment scenario \(for example, where the main entity set is from a parameterized entity\), you can maintain the annotations as shown in the following sample code:

    > ### Sample Code:  
    > XML Annotation \(containment scenario\): /Customer/Set/\_PartnerItems
    > 
    > ```xml
    > <Annotations Target="SAP__self.Container/ItemPartner">
    >    <Annotation Term="SAP__capabilities.SearchRestrictions">
    >       <Record>
    >          <PropertyValue Property="Searchable" Bool="false" />
    >       </Record>
    >    </Annotation>
    > </Annotations>
    > ```

    > ### Sample Code:  
    > ABAP CDS Annotation
    > 
    > No ABAP CDS annotation sample is available. Please use the local XML annotation.

    > ### Sample Code:  
    > CAP CDS Annotation \(containment scenario\)
    > 
    > ```
    > entity ItemPartner @(
    >    Capabilities:{
    >       SearchRestrictions : {Searchable : false}
    >    }
    > )
    > ```


**Related Information**  


[Configuring Tables](configuring-tables-f4eb70f.md "You can use the annotations and entries in the manifest.json to control various aspects of tables.")

[Setting the Table Type](setting-the-table-type-7f844f1.md "In the manifest.json file, and through annotations, you can control which table type is rendered in the list report and on the object page.")

[Tables: Which One Should I Choose?](../10_More_About_Controls/tables-which-one-should-i-choose-148892f.md "The libraries provided by SAPUI5 contain various different table controls that are suitable for different use cases. The table below outlines which table controls are available, and what features are supported by each one.")

[Enabling Multiple Selection in Tables](enabling-multiple-selection-in-tables-116b5d8.md "This feature enables you to configure whether end users can select a single row or multiple rows in a table, while triggering table toolbar actions that require context.")
