---
title: scheme
description: 
published: true
date: 2022-04-21T05:54:49.811Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:24:23.763Z
---

# DataGridLight scheme



```plantuml
digraph datagridlight {
    node[shape=record]
    ranksep=2.5
    nodesep=1

    subgraph cluster_1 {
        DataGridLight[
            URL="https://github.com/DevExpress/DevExtreme/blob/22_1/js/renovation/ui/grids/data_grid_light/data_grid_light.tsx"
            label="{
                DataGridLight |
                wrapped in Widget |
                @Provider(PluginContext)
            }"
            style=filled
        ]

        DataGridLight -> TableHeader
        DataGridLight -> TableContent
        DataGridLight -> Footer
        DataGridLight -> children
        
        TableHeader -> HeaderRow
        TableContent -> DataRow
        
        TableHeader[
            label="{
                TableHeader |
                wrapped in Table |
                { columns | Column[] | oneWay }
            }"
        ]
        TableContent[
            label="{
                TableContent |
                wrapped in Table |
                { columns | Column[] | oneWay } |
                { dataSource | RowData[] | oneWay }
            }"
        ]
        children[
            label="{
                children |
                used for nested modules
            }"
        ]
        HeaderRow[
            label="{
                HeaderRow |
                { columns | Column[] | oneWay }
            }"
        ]
        DataRow[
            label="{
                DataRow |
                { data | RowData | oneWay } |
                { rowIndex | number | oneWay } |
                { columns | Column[] | oneWay }
            }"
        ]
        
        label="Hard-coded components"
    }
    
    Footer -> Pager[label="Via placeholder" style=dotted]
    
    Pager->BasePager
    
    BasePager[
        label="{
            Pager |
            js\\renovation\\ui\\pager\\pager.tsx
        }"
    ]
    
    Paging[
        label="{
            Paging |
            { pageSize | number \| 'all' | twoWay } |
            { pageIndex | number | twoWay } |
            { enabled | boolean | oneWay }
        }"
        style=filled
        pos="100,100!"
    ]
    
    subgraph cluster_paging {
        PageCount[
            shape=Mrecord
            label="{
                PageCount |
                { number | createSelector() }
            }"
        ]
        PageIndex[
            shape=Mrecord
            label="{
                PageIndex |
                { number | createValue() }
            }"
        ]
        PageSize[
            shape=Mrecord
            label="{
                PageSize |
                { number \| 'all' | createValue() }
            }"
        ]
        SetPageIndex[
            shape=Mrecord
            label="{
                SetPageIndex |
                { (number) \=\> void | createValue() }
            }"
        ]
        SetPageSize[
            shape=Mrecord
            label="{
                SetPageSize |
                { (number \| 'all') \=\> void | createValue() }
            }"
        ]
        
        label="Paging plugins"
    }
    Paging -> PageIndex[
        style="dashed"
        label="set"
    ]
    PageIndex -> Pager[
        style="dashed"
        label="watch"
    ]
    Paging -> PageSize[
        style="dashed"
        label="set"
    ]
    PageSize -> Pager[
        style="dashed"
        label="watch"
    ]
    Paging -> SetPageIndex[
        style="dashed"
        label="set"
    ]
    SetPageIndex -> Pager[
        style="dashed"
        label="call"
    ]
    Paging -> SetPageSize[
        style="dashed"
        label="set"
    ]
    SetPageSize -> Pager[
        style="dashed"
        label="call"
    ]
    Paging -> PageCount[
        style="dashed"
        label="set"
    ]
    PageCount -> Pager[
        style="dashed"
        label="watch"
    ]
    DataGridLight -> TotalCount[
        style="dashed"
        label="sets"
    ]
    TotalCount -> Pager[
        style="dashed"
        label="watch"
    ]
    
    TotalCount[
        shape=Mrecord
        label="{
            TotalCount |
            { number | createSelector() }
        }"
    ]
    
    VisibleItems[
        shape=Mrecord
        label="{
            { VisibleItems | createGetter() } |
            { RowData[] }
        }"
    ]
    
    VisibleColumns[
        shape=Mrecord
        label="{
            { VisibleColumns | createGetter() } |
            { RowData[] }
        }"
    ]
    
    VisibleColumns -> DataGridLight[
        label="watch"
        style="dashed"
    ]
    
    DataGridLight -> VisibleColumns[
        label="extend\norder: -1\n(inits with user columns)"
        style=dashed
    ]

    DataGridLight -> VisibleItems[
        label="extend\norder: -1\n(inits with dataSource)"
        style=dashed
    ]
    
    VisibleItems -> DataGridLight[
        label="watch"
        style="dashed"
    ]
    
    Paging -> VisibleItems[
        label="extend\norder: 1"
        style="dashed"
    ]
    
    Pager[
        label="{
            Pager |
            many oneway props
        }"
        style=filled
    ]
    
    Selection[
        label="{
            Selection |
            { selectedRowKeys | KeyExpr[] | twoWay } |
            { mode | 'single' \| 'multiple' \| 'none' | oneWay }
        }"
        style=filled
    ]
    
    Selection -> VisibleColumns[
        label="extend\nadds checkboxes\norder: 1"
        style="dashed"
    ]
    
    VisibleItems -> Selection[
        label="gets"
        style="dashed"
    ]
    
    KeyExprPlugin[
        shape=Mrecord
        label="{
            KeyExprPlugin |
            { KeyExpr | createValue() }
        }"
    ]
    
    DataGridLight -> KeyExprPlugin[
        label="sets"
        style="dashed"
    ]
    KeyExprPlugin -> Selection[
        label="watch"
        style="dashed"
    ]
    
    DataSource[
        shape=Mrecord
        label="{
            DataSource |
            { RowData[] | createValue() }
        }"
    ]
    
    DataGridLight -> DataSource[
        label="sets"
        style="dashed"
    ]
    DataSource -> Selection[
        label="watch"
        style="dashed"
    ]
    
    DataRowClassesGetter[
        shape=Mrecord
        label="{
            DataRowClassesGetter |
            { (RowData) \=\> Record(string, boolean) | createGetter() }
        }"
    ]

    DataRowClassesGetter->DataRow[
        style=dashed
        label="watch"
    ]
    Selection->DataRowClassesGetter[
        style=dashed
        label="extends\norder=1\nadds 'dx-selection' class"
    ]
    
    DataRowPropertiesGetter[
        shape=Mrecord
        label="{
            DataRowPropertiesGetter |
            { (RowData) \=\> Record(string, string) | createGetter() }
        }"
    ]

    DataRowPropertiesGetter->DataRow[
        style=dashed
        label="watch"
    ]
    Selection->DataRowPropertiesGetter[
        style=dashed
        label="extends\norder=1\nadds 'aria-selected'"
    ]
}
```

###### description

- rectangle records --- jsx components
    - gray --- public jsx components
- rounded records --- plugin interface
- simple arrows --- composition
- dashed arrows --- using a plugin
