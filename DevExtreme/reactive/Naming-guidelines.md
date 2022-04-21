---
title: Naming guidelines
description: 
published: true
date: 2022-04-21T11:18:08.534Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:58:22.160Z
---

## Plugins

- adequate name that clearly defines the plugin's mission
- general plugins that can influence a number of other plugins (like DragDropPropvider) should end with '...Provider'
- state plugins should end with '...State'
- plugins that are responsible for data processing should start with 'integrated...'
- plugins implementing additional features close to other plugins should include the main plugin name (e.g. TableHeaderRow, TableColumnResizing, etc.)

## Actions

- adequate name that clearly defines the meaning
- avoid 'xxxAction', 'xxxExecutor' and another water in action name parts
- don't miss to add valuable parts to the action name. For example, in the 'changeTableColumnWidth' action, we can't remove the 'xxxTableXXX' part because the Grid's column can't have width.
- use 'toggleXXX' as a name if the main purpose of the action is to toggle something. Use the 'state' name as a parameter name for this.
- use 'setXXX' as an action name if the action is only setting something. This also means that setting should be applied to a whole object. E.g. the 'setCurrentPage' action.
- use 'changeXXX' as an action name in case of changing(adding/removing/toggling) or partial update allowed by one action. E.g. the 'changeColumnSorting' action.
- use 'draftXXX' as an action name in case of change used for preview. To cancel draft, use the following pattern: 'cancelXXXDraft'. E.g. changeTableColumnWidth/draftTableColumnWidth/cancelTableColumnWidthDraft, changeColumnGrouping/draftColumnGrouping/cancelColumnGroupingDraft.

## Templates

- adequate name that clearly defines the meaning
- avoid 'xxxView', 'xxxPlaceholder' and another water in template name parts
- use 'xxxContainer' as a name if it wraps or contents something
- use 'xxxContent' as a name of something that will be inside something

##Getters

All names must display the essence that is contained in them. Like `names`, `ids`, `rows`, `columns` etc.
Prefer simple data structures. For example array instead of set.

1. Boolean
`xxxEnabled` for properties that we can set a value draggingEnabled
getternameAvailable for properties that we can not set a value selectAllAvailable
`xxx + past tense` if don’t contain into the two first rules allSelected
2. Number
Nouns and adjectives
totalCount
3. Functions
`isXXX` if return a boolean value
isGroupRow
`getXXX` if return an any value
getCellValue
4. Array of IDs
`xxxIds`
	editedRowIds
5. Array of Rows
`xxxRows`
	addedRows
6. Array of any
`xxx - nouns into plural or with -ing`
	filters, grouping
7. Array of preview values
`draftXXX`
	draftGrouping

## Dependent Properties

- `XXX` for property name like a getter name
- `defaultXXX` for started property value
- `onXXXChange` spelling for an event