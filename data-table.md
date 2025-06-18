## DataTable Component Documentation

## 1. Introduction

The `DataTable` component from GENDS is a highly flexible and customizable React component designed for displaying tabular data. It leverages `@tanstack/react-table` for efficient table management and provides a rich set of features including sorting, row selection, column pinning, sub-tables, virtualization for large datasets, and various customization options for headers, footers, and cell rendering. It is built to be integrated seamlessly into MCP server applications, offering a robust solution for presenting complex data.

### Key Features:

- **Data Display**: Efficiently renders large datasets.
- **Sorting**: Built-in sorting functionality for columns.
- **Row Selection**: Supports single and multiple row selection.
- **Column Pinning**: Allows pinning columns to the left or right for improved readability.
- **Sub-tables**: Enables hierarchical data display with expandable rows and nested tables.
- **Virtualization**: Optimizes performance for large datasets by rendering only visible rows.
- **Customizable Layout**: Provides slots for custom headers, footers, and action bars.
- **Loading States**: Includes shimmer loading for a better user experience.
- **Truncation and Wrapping**: Controls for text overflow within cells.

## 2. Installation

To use the `DataTable` component in your MCP server application, you need to install the necessary dependencies and import the component from the GENDS project.

### Prerequisites

Ensure you have Node.js and npm/yarn installed.

### Installation Steps

1.  **Install GENDS Package (if not already installed)**:

    ```bash
    npm install @gends/ui-components @tanstack/react-table @tanstack/react-virtual
    # or
    yarn add @gends/ui-components @tanstack/react-table @tanstack/react-virtual
    ```

2.  **Import `DataTable` Component**:

    You can import the `DataTable` component and its related types directly from the GENDS package:

    ```typescript
    import { DataTable, ColumnDef } from "gends";
    // or if directly from the component path
    import { DataTable } from "gends";
    import { ColumnDef } from "gends";
    ```

    For type definitions, you might also need to import `Table` and `Row` from `@tanstack/react-table`:

    ```typescript
    import { Table, Row } from "gends";
    ```

## 3. API Reference (DataTableProps)

The `DataTable` component accepts the following props to customize its behavior and appearance. The generic type `TData` represents the shape of the data objects in your table.

```typescript
interface DataTableProps<TData extends Record<string, any>> {
  table: TanTable<TData>;
  originalColumns?: ColumnDef<TData>[];
  onRowSelection?: (selected: TData[]) => void;
  tabsComponent?: React.ReactNode;
  search?: React.ReactNode;
  filters?: React.ReactNode;
  tableFooter?: React.ReactNode;
  stickyFooter?: boolean;
  showTableFooter?: boolean;
  onSortChange?: (sort: { id: string; desc: boolean } | null) => void;
  enableRowSelection?: boolean;
  showColumnDivider?: boolean;
  subTableColumnDef?: ColumnDef<Record<string, unknown>>[];
  SubTableComponent?: React.ComponentType<{ data: Record<string, unknown>[] }>;
  tableHeight?: string;
  emptyStateHeight?: string;
  headerTopRow?: React.ReactNode;
  headerBottomRow?: React.ReactNode;
  showHeaderTopRow?: boolean;
  showHeaderBottomRow?: boolean;
  children?: React.ReactNode;
  subRowKey?: string;
  subTableKey?: string;
  showHeaderMiddleRow?: boolean;
  headerMiddleRow?: React.ReactNode;
  renderRowActions?: (row: Row<TData>) => React.ReactNode;
  truncateAll?: boolean;
  truncateColumns?: string[];
  wrapAll?: boolean;
  wrapColumns?: string[];
  isLoading?: boolean;
  shimmerRowCount?: number;
  showOuterBorder?: boolean;
  dataTableContainerProps?: React.ComponentProps<"div">;
  enableVirtualization?: boolean;
  estimateRowSize?: number;
  overscan?: number;
  paginationContainerProps?: React.ComponentProps<"div">;
}
```

### Props Details

| Prop Name                  | Type                                                       | Default Value | Description                                                                                                                                                                               |
| :------------------------- | :--------------------------------------------------------- | :------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `table`                    | `TanTable<TData>`                                          | `N/A`         | **Required**. The table instance created using `useReactTable` from `@tanstack/react-table`. This object contains all the table state and methods.                                        |
| `originalColumns`          | `ColumnDef<TData>[]`                                       | `[]`          | Original user-defined column definitions. Used internally to detect custom cell renderers and for column management.                                                                      |
| `onRowSelection`           | `(selected: TData[]) => void`                              | `undefined`   | Callback function triggered when row selection changes. Receives an array of selected data objects.                                                                                       |
| `tabsComponent`            | `React.ReactNode`                                          | `undefined`   | A React node to be rendered as a tabs component within the table toolbar.                                                                                                                 |
| `search`                   | `React.ReactNode`                                          | `undefined`   | A React node to be rendered as a search input component within the table toolbar.                                                                                                         |
| `filters`                  | `React.ReactNode`                                          | `undefined`   | A React node to be rendered as a filters component within the table toolbar.                                                                                                              |
| `tableFooter`              | `React.ReactNode`                                          | `undefined`   | A React node to be rendered as the table footer content.                                                                                                                                  |
| `stickyFooter`             | `boolean`                                                  | `true`        | If `true`, the table footer will stick to the bottom of the table when scrolling.                                                                                                         |
| `showTableFooter`          | `boolean`                                                  | `undefined`   | If `true`, the table footer will be rendered.                                                                                                                                             |
| `onSortChange`             | `(sort: { id: string; desc: boolean } \| null) => void`    | `undefined`   | Callback function triggered when sorting changes. Provides the sorted column ID and direction.                                                                                            |
| `enableRowSelection`       | `boolean`                                                  | `false`       | If `true`, enables row selection functionality for the table.                                                                                                                             |
| `showColumnDivider`        | `boolean`                                                  | `false`       | If `true`, displays a visual divider between columns.                                                                                                                                     |
| `subTableColumnDef`        | `ColumnDef<Record<string, unknown>>[]`                     | `undefined`   | Column definitions for sub-tables. Used when `SubTableComponent` is not provided.                                                                                                         |
| `SubTableComponent`        | `React.ComponentType<{ data: Record<string, unknown>[] }>` | `undefined`   | A custom React component to render sub-tables. Receives `data` as props.                                                                                                                  |
| `tableHeight`              | `string`                                                   | `undefined`   | Sets a fixed height for the table container. Useful for controlling table dimensions within a layout.                                                                                     |
| `emptyStateHeight`         | `string`                                                   | `'200px'`     | Sets the height of the empty state message when no data is available.                                                                                                                     |
| `headerTopRow`             | `React.ReactNode`                                          | `undefined`   | A React node to be rendered in the top row of the table header.                                                                                                                           |
| `headerBottomRow`          | `React.ReactNode`                                          | `undefined`   | A React node to be rendered in the bottom row of the table header.                                                                                                                        |
| `showHeaderTopRow`         | `boolean`                                                  | `undefined`   | If `true`, the `headerTopRow` will be rendered.                                                                                                                                           |
| `showHeaderBottomRow`      | `boolean`                                                  | `undefined`   | If `true`, the `headerBottomRow` will be rendered.                                                                                                                                        |
| `children`                 | `React.ReactNode`                                          | `undefined`   | Any React nodes passed as children will be rendered within the `DataTableContainer`. This is typically where the main table content (e.g., `Table`, `TableHeader`, `TableBody`) would go. |
| `subRowKey`                | `string`                                                   | `'subRows'`   | The key in your data object that contains nested sub-rows for expandable rows.                                                                                                            |
| `subTableKey`              | `string`                                                   | `'subTable'`  | The key in your data object that contains data for a sub-table.                                                                                                                           |
| `showHeaderMiddleRow`      | `boolean`                                                  | `undefined`   | If `true`, the `headerMiddleRow` will be rendered.                                                                                                                                        |
| `headerMiddleRow`          | `React.ReactNode`                                          | `undefined`   | A React node to be rendered in the middle row of the table header.                                                                                                                        |
| `renderRowActions`         | `(row: Row<TData>) => React.ReactNode`                     | `undefined`   | A function that receives the `row` object and returns React nodes to be rendered as row-specific actions (e.g., a menu button).                                                           |
| `truncateAll`              | `boolean`                                                  | `true`        | If `true`, all cell content will be truncated with an ellipsis if it overflows. A tooltip will show the full content on hover.                                                            |
| `truncateColumns`          | `string[]`                                                 | `[]`          | A list of column IDs for which cell content should be truncated. Overrides `truncateAll` for specified columns.                                                                           |
| `wrapAll`                  | `boolean`                                                  | `false`       | If `true`, all cell content will wrap to multiple lines if it overflows.                                                                                                                  |
| `wrapColumns`              | `string[]`                                                 | `[]`          | A list of column IDs for which cell content should wrap. Overrides `wrapAll` for specified columns.                                                                                       |
| `isLoading`                | `boolean`                                                  | `false`       | If `true`, displays a shimmer loading animation over the table rows.                                                                                                                      |
| `shimmerRowCount`          | `number`                                                   | `5`           | The number of shimmer rows to display when `isLoading` is `true`.                                                                                                                         |
| `showOuterBorder`          | `boolean`                                                  | `false`       | If `true`, displays an outer border around the entire table.                                                                                                                              |
| `dataTableContainerProps`  | `React.ComponentProps<"div">`                              | `{}`          | Additional props to pass to the internal `DataTableContainer` component (e.g., `className`, `style`).                                                                                     |
| `enableVirtualization`     | `boolean`                                                  | `false`       | If `true`, enables row virtualization for improved performance with large datasets.                                                                                                       |
| `estimateRowSize`          | `number`                                                   | `44`          | Estimated height of each row in pixels. Important for accurate virtualization calculations.                                                                                               |
| `overscan`                 | `number`                                                   | `5`           | The number of items to render outside of the visible area during virtualization. Helps prevent blank spaces during fast scrolling.                                                        |
| `paginationContainerProps` | `React.ComponentProps<"div">`                              | `{}`          | Additional props to pass to the internal `TablePagination` component (e.g., `className`, `style`).                                                                                        |

## 4. Usage Examples

This section provides practical examples demonstrating how to integrate and use the `DataTable` component in various scenarios.

### 4.1 Basic Usage

This example demonstrates a basic setup of the `DataTable` with sorting, row selection, and custom header/footer elements. It utilizes the `useDataTable` hook (presumably from GENDS as well) to manage the `@tanstack/react-table` instance.

```typescript
// ExampleTable.tsx
"use client";

import React, { useState, useMemo, useCallback } from "react";
import { DataTable } from "gends";
import { useDataTable } from "gends";
import { TabsRow } from "gends";
import { FilterPills } from "gends";
import { Pagination } from "gends";
import { userData } from "gends";
import { Button } from "gends";
import { CustomASNTable } from "gends";
import {
  DataTableActionBar,
  DataTableActionBarSelection,
  DataTableActionBarAction,
  DataTableActionBarOverflow,
} from "gends";

import { ColumnDef, SortingState, Updater } from "@tanstack/react-table";
import type { UserRow, ASNRow } from "gends";

// flat columns & groupedColumns imported from your definitions
import { columns, groupedColumns } from "gends";
import { ColumnManagerDropdown } from "gends";

export function ExampleTable() {
  // ---- UI toggles ----
  const [enableRowSelection, setEnableRowSelection] = useState(false);
  const [showColumnDivider, setShowColumnDivider] = useState(false);
  const [showColGroup, setShowColGroup] = useState(false);
  const [stickyFooter, setStickyFooter] = useState(true);

  // ---- sorting state ----
  const [sortParam, setSortParam] = useState<string>(""); // e.g. "id.asc"
  const sorting: SortingState = useMemo(() => {
    if (!sortParam) return [];
    const [id, dir] = sortParam.split(".");
    return [{ id, desc: dir === "desc" }];
  }, [sortParam]);
  const onSortingChange = useCallback(
    (next: Updater<SortingState>) => {
      const newState = typeof next === "function" ? next(sorting) : next;
      const head = newState[0];
      if (head) setSortParam(`${head.id}.${head.desc ? "desc" : "asc"}`);
      else setSortParam("");
    },
    [sorting]
  );

  // ---- build the TanStack table instance ----
  const { table, originalColumns } = useDataTable<UserRow>({
    data: userData,
    columns: showColGroup ? groupedColumns : columns,
    pageCount: 1,
    sorting,
    onSortingChange,
    enableRowSelection,
    showExpandRowIcon: true,
    // manualPagination/filtering/sorting are already set in the hook
    defaultColumn: { size: 50, minSize: 30, maxSize: 600 },
  });

  // ---- pull out selected rows for the action bar ----
  const selectedRows = table.getSelectedRowModel().rows.map((r) => r.original);

  return (
    <div className="p-5 bg-gray-50 space-y-4">
      {/* Controls */}
      <div className="flex flex-wrap gap-2">
        <Button onClick={() => setEnableRowSelection((v) => !v)}>
          Toggle Row Selection
        </Button>
        <Button
          onClick={() => setShowColumnDivider((v) => !v)}
          variant="outline"
        >
          Toggle Borders
        </Button>
        <Button onClick={() => setShowColGroup((v) => !v)}>
          Toggle Grouping
        </Button>
      </div>

      {/* DataTable */}
      <DataTable<UserRow>
        table={table}
        originalColumns={originalColumns}
        enableRowSelection={enableRowSelection}
        showColumnDivider={showColumnDivider}
        tableHeight={stickyFooter ? "60vh" : "auto"}
        showTableFooter
        stickyFooter={stickyFooter}
        tableFooter={
          <Pagination
            currentPage={table.getState().pagination.pageIndex + 1}
            totalPages={table.getPageCount()}
            pageSize={table.getState().pagination.pageSize}
            onPageChange={(p) => table.setPageIndex(p - 1)}
            onPageSizeChange={(size) => table.setPageSize(size)}
            className="w-full"
            table={table}
          />
        }
        headerTopRow={
          <div className="border-b bg-white px-4 py-2">
            <TabsRow table={table} />
            <div className="flex items-center gap-2">
              <ColumnManagerDropdown table={table} />
            </div>
          </div>
        }
        showHeaderTopRow
        headerBottomRow={
          <div className="px-4 py-2">
            <FilterPills table={table} />
          </div>
        }
        showHeaderBottomRow
        SubTableComponent={({ data }) => (
          <CustomASNTable data={data as ASNRow[]} />
        )}
        wrapAll={false}
        truncateAll={true}
      >
        {/* Action Bar */}
        <DataTableActionBar table={table}>
          <DataTableActionBarSelection table={table} />
          <DataTableActionBarAction
            tooltip="Delete rows"
            onClick={() => console.log("Delete", selectedRows)}
          >
            Delete
          </DataTableActionBarAction>
          <DataTableActionBarAction
            tooltip="Archive rows"
            onClick={() => console.log("Archive", selectedRows)}
          >
            Archive
          </DataTableActionBarAction>
          <DataTableActionBarOverflow
            items={[
              {
                label: "Export CSV",
                onClick: () => console.log("Export CSV"),
              },
              {
                label: "Mark as Read",
                onClick: () => console.log("Mark as Read"),
              },
            ]}
          />
        </DataTableActionBar>
      </DataTable>
    </div>
  );
}
```

**Explanation:**

- **`useDataTable` Hook**: This custom hook simplifies the setup of `@tanstack/react-table`, handling common configurations like pagination, sorting, and filtering. It returns the `table` instance and `originalColumns` which are then passed to the `DataTable` component.
- **`table` Prop**: The core prop, it's the instance of your table created by `useReactTable` (or `useDataTable` in this case).
- **`enableRowSelection`**: A boolean prop that enables or disables the checkbox for row selection.
- **`showColumnDivider`**: A boolean prop to toggle the visibility of column borders.
- **`tableHeight` and `stickyFooter`**: Used to control the table's height and make the footer sticky, useful for tables within limited vertical space.
- **`tableFooter`**: A `React.ReactNode` that allows you to inject any component into the table's footer. Here, a `Pagination` component is used.
- **`headerTopRow` and `headerBottomRow`**: These `React.ReactNode` props allow you to inject custom content into the top and bottom sections of the table header. This example uses `TabsRow`, `ColumnManagerDropdown`, and `FilterPills` for advanced table controls.
- **`SubTableComponent`**: Demonstrates how to provide a custom component (`CustomASNTable`) to render nested sub-tables when a row is expanded.
- **`truncateAll` and `wrapAll`**: Control how cell content is displayed when it overflows. `truncateAll` (default `true`) truncates text with an ellipsis and shows a tooltip on hover, while `wrapAll` (default `false`) allows text to wrap.
- **`DataTableActionBar`**: This component (and its sub-components `DataTableActionBarSelection`, `DataTableActionBarAction`, `DataTableActionBarOverflow`) provides a flexible way to implement actions that apply to selected rows, appearing conditionally when rows are selected.

### 4.2 Editable Table

The `DataTable` component can be used to create editable tables by providing custom cell renderers that include input components. GENDS provides several `Editable*Cell` components to facilitate this.

```typescript
// Example Editable Table with GenDS Components
import React, { useState, useMemo, useCallback } from "react";
import { ColumnDef } from "gends";
import {
  DataTable,
  useDataTable,
  EditableTextCell,
  EditableNumberCell,
  EditableDropdownCell,
  EditableCheckboxCell,
  EditableDateCell,
  type DropdownOption,
} from "gends"; // Assuming GENDS package export
import { Pagination } from "gends"; // Adjust path as per your project structure

// Sample data interface
interface EditableRow {
  id: number;
  name: string;
  email: string;
  age: number;
  department: string;
  status: "active" | "inactive" | "pending";
  priority: "low" | "medium" | "high";
  isActive: boolean;
  startDate: Date | null;
  salary: number;
}

// Sample data
const generateSampleData = (): EditableRow[] => {
  const departments = ["Engineering", "Marketing", "Sales", "HR", "Finance"];
  const statuses: ("active" | "inactive" | "pending")[] = [
    "active",
    "inactive",
    "pending",
  ];
  const priorities: ("low" | "medium" | "high")[] = ["low", "medium", "high"];

  return Array.from({ length: 20 }, (_, i) => ({
    id: i + 1,
    name: `Employee ${i + 1}`,
    email: `employee${i + 1}@company.com`,
    age: 25 + (i % 15),
    department: departments[i % departments.length],
    status: statuses[i % statuses.length],
    priority: priorities[i % priorities.length],
    isActive: i % 2 === 0,
    startDate:
      i % 3 === 0 ? new Date(Date.now() - i * 30 * 24 * 60 * 60 * 1000) : null,
    salary: 50000 + i * 5000,
  }));
};

export function EditableTableExample() {
  const [data, setData] = useState<EditableRow[]>(generateSampleData);
  const [pagination, setPagination] = useState({ pageIndex: 0, pageSize: 10 });

  // Dropdown options
  const departmentOptions: DropdownOption[] = [
    { id: "engineering", label: "Engineering", value: "Engineering" },
    { id: "marketing", label: "Marketing", value: "Marketing" },
    { id: "sales", label: "Sales", value: "Sales" },
    { id: "hr", label: "HR", value: "HR" },
    { id: "finance", label: "Finance", value: "Finance" },
  ];

  const statusOptions: DropdownOption[] = [
    { id: "active", label: "Active", value: "active" },
    { id: "inactive", label: "Inactive", value: "inactive" },
    { id: "pending", label: "Pending", value: "pending" },
  ];

  const priorityOptions: DropdownOption[] = [
    { id: "low", label: "Low", value: "low" },
    { id: "medium", label: "Medium", value: "medium" },
    { id: "high", label: "High", value: "high" },
  ];

  // Handle cell updates
  const handleCellUpdate = useCallback(
    (rowIndex: number, field: keyof EditableRow, value: any) => {
      setData((prevData) => {
        const newData = [...prevData];
        const actualIndex =
          pagination.pageIndex * pagination.pageSize + rowIndex;
        if (newData[actualIndex]) {
          newData[actualIndex] = { ...newData[actualIndex], [field]: value };
        }
        return newData;
      });
      console.log(`Updated row ${rowIndex}, field ${field}:`, value);
    },
    [pagination.pageIndex, pagination.pageSize]
  );

  // Column definitions with editable cells
  const columns = useMemo<ColumnDef<EditableRow>[]>(
    () => [
      {
        accessorKey: "id",
        header: "ID",
        size: 60,
        cell: ({ getValue }) => getValue(), // Read-only
      },
      {
        accessorKey: "name",
        header: "Name",
        cell: ({ row, getValue }) => (
          <EditableTextCell
            value={String(getValue() || "")}
            onChange={(value) => handleCellUpdate(row.index, "name", value)}
            placeholder="Enter name"
            onSave={() => console.log("Name saved for row", row.index)}
          />
        ),
      },
      {
        accessorKey: "email",
        header: "Email",
        cell: ({ row, getValue }) => (
          <EditableTextCell
            value={String(getValue() || "")}
            onChange={(value) => handleCellUpdate(row.index, "email", value)}
            type="email"
            placeholder="Enter email"
            onSave={() => console.log("Email saved for row", row.index)}
          />
        ),
      },
      {
        accessorKey: "age",
        header: "Age",
        size: 80,
        cell: ({ row, getValue }) => (
          <EditableTextCell
            value={Number(getValue() || 0)}
            onChange={(value) =>
              handleCellUpdate(row.index, "age", Number(value))
            }
            type="number"
            placeholder="Enter age"
            onSave={() => console.log("Age saved for row", row.index)}
          />
        ),
      },
      {
        accessorKey: "department",
        header: "Department",
        cell: ({ row, getValue }) => (
          <EditableDropdownCell
            value={String(getValue() || "")}
            onChange={(value) =>
              handleCellUpdate(row.index, "department", value)
            }
            options={departmentOptions}
            placeholder="Select department"
            onSave={() => console.log("Department saved for row", row.index)}
          />
        ),
      },
      {
        accessorKey: "status",
        header: "Status",
        cell: ({ row, getValue }) => (
          <EditableDropdownCell
            value={String(getValue() || "")}
            onChange={(value) => handleCellUpdate(row.index, "status", value)}
            options={statusOptions}
            placeholder="Select status"
            onSave={() => console.log("Status saved for row", row.index)}
          />
        ),
      },
      {
        accessorKey: "priority",
        header: "Priority",
        cell: ({ row, getValue }) => (
          <EditableDropdownCell
            value={String(getValue() || "")}
            onChange={(value) => handleCellUpdate(row.index, "priority", value)}
            options={priorityOptions}
            placeholder="Select priority"
            onSave={() => console.log("Priority saved for row", row.index)}
          />
        ),
      },
      {
        accessorKey: "isActive",
        header: "Active",
        size: 80,
        cell: ({ row, getValue }) => (
          <EditableCheckboxCell
            value={Boolean(getValue())}
            onChange={(value) => handleCellUpdate(row.index, "isActive", value)}
            onSave={() => console.log("Active status saved for row", row.index)}
          />
        ),
      },
      {
        accessorKey: "startDate",
        header: "Start Date",
        cell: ({ row, getValue }) => (
          <EditableDateCell
            value={getValue() as Date | null}
            onChange={(value) =>
              handleCellUpdate(row.index, "startDate", value)
            }
            placeholder="Select start date"
            onSave={() => console.log("Start date saved for row", row.index)}
          />
        ),
      },
      {
        accessorKey: "salary",
        header: "Salary",
        cell: ({ row, getValue }) => (
          <EditableTextCell
            value={Number(getValue() || 0)}
            onChange={(value) =>
              handleCellUpdate(row.index, "salary", Number(value))
            }
            type="number"
            placeholder="Enter salary"
            onSave={() => console.log("Salary saved for row", row.index)}
          />
        ),
      },
    ],
    [handleCellUpdate, departmentOptions, statusOptions, priorityOptions]
  );

  // Get paginated data
  const paginatedData = useMemo(() => {
    const start = pagination.pageIndex * pagination.pageSize;
    const end = start + pagination.pageSize;
    return data.slice(start, end);
  }, [data, pagination]);

  const { table } = useDataTable<EditableRow>({
    data: paginatedData,
    columns,
    pageCount: Math.ceil(data.length / pagination.pageSize),
    pagination,
    onPaginationChange: setPagination,
    enableRowSelection: true,
    getRowId: (row) => String(row.id),
  });

  return (
    <div className="p-6 space-y-4">
      <div className="space-y-2">
        <h2 className="text-2xl font-bold">Editable Table Example</h2>
        <p className="text-gray-600">
          Click on any cell to edit. Changes are saved automatically when you
          click outside or press Enter. Press Escape to cancel editing.
        </p>
      </div>

      <DataTable<EditableRow>
        table={table}
        showColumnDivider
        tableHeight="600px"
        showTableFooter
        tableFooter={
          <Pagination
            currentPage={pagination.pageIndex + 1}
            totalPages={table.getPageCount()}
            pageSize={pagination.pageSize}
            onPageChange={(page) =>
              setPagination((prev) => ({ ...prev, pageIndex: page - 1 }))
            }
            onPageSizeChange={(size) =>
              setPagination((prev) => ({
                ...prev,
                pageSize: size,
                pageIndex: 0,
              }))
            }
            className="w-full"
          />
        }
      />

      <div className="mt-4 p-4 bg-gray-50 rounded-lg">
        <h3 className="font-semibold mb-2">Features Demonstrated:</h3>
        <ul className="list-disc list-inside space-y-1 text-sm text-gray-700">
          <li>
            <strong>Text Input:</strong> Name, Email fields with click-to-edit
          </li>
          <li>
            <strong>Number Input:</strong> Age, Salary fields with numeric
            validation
          </li>
          <li>
            <strong>Dropdown Selection:</strong> Department, Status, Priority
            with predefined options
          </li>
          <li>
            <strong>Checkbox:</strong> Active status with immediate toggle
          </li>
          <li>
            <strong>Date Picker:</strong> Start Date with calendar selection
          </li>
          <li>
            <strong>Auto-save:</strong> Changes saved on blur or Enter key
          </li>
          <li>
            <strong>Cancel editing:</strong> Press Escape to cancel changes
          </li>
          <li>
            <strong>Visual feedback:</strong> Hover states and edit indicators
          </li>
        </ul>
      </div>
    </div>
  );
}
```

**Explanation:**

- **`EditableRow` Interface**: Defines the structure of the data for the editable table.
- **`handleCellUpdate` Function**: A callback function that updates the component's state (`data`) when a cell's value changes. This is where you would typically integrate with your backend API to persist changes.
- **Column Definitions**: Each column's `cell` property is rendered using one of the provided `Editable*Cell` components (`EditableTextCell`, `EditableDropdownCell`, `EditableCheckboxCell`, `EditableDateCell`). These components manage their own editing state and call the `onChange` prop when a value is committed.
- **`EditableTextCell`**: A versatile cell for text and number inputs. It supports `text`, `number`, and `email` types.
- **`EditableDropdownCell`**: For selecting values from a predefined list of options.
- **`EditableCheckboxCell`**: For boolean values, providing a simple checkbox.
- **`EditableDateCell`**: For selecting dates using a date picker.
- **`onSave` and `onCancel` Props**: These optional callbacks on the editable cell components allow you to perform actions (e.g., API calls) when an edit is saved or cancelled.

### 4.3 Virtualized Table for Large Datasets

The `DataTable` component supports virtualization using `@tanstack/react-virtual` to efficiently handle large datasets (thousands or tens of thousands of rows). Virtualization renders only the visible rows in the viewport, significantly improving performance and memory efficiency.

#### When to Use Virtualization

- **Use for**: 1,000+ rows
- **Use for**: Real-time data updates
- **Use for**: Complex cell renderers
- **Avoid for**: < 100 rows (unnecessary overhead)
- **Avoid for**: Variable row heights (use fixed heights)

#### Basic Usage

To enable virtualization, set `enableVirtualization` to `true` and provide a `tableHeight`.

```typescript
import { DataTable, useDataTable } from "gends";
import { ColumnDef } from "gends";

// Assume largeDataset is an array of 10,000+ items
const largeDataset: YourDataType[] = [...];

const columns: ColumnDef<YourDataType>[] = [
  // Your column definitions with fixed sizes for better performance
  {
    accessorKey: "id",
    header: "ID",
    size: 60,
  },
  {
    accessorKey: "name",
    header: "Name",
    size: 200,
    maxSize: 200, // Prevents layout shifts
  },
  // ... other columns
];

function VirtualizedTable() {
  const { table, originalColumns } = useDataTable<YourDataType>({
    data: largeDataset,
    columns,
    pageCount: Math.ceil(largeDataset.length / 50), // Example pagination
  });

  return (
    <DataTable
      table={table}
      originalColumns={originalColumns}
      enableVirtualization={true}
      tableHeight="600px" // Required for virtualization
      estimateRowSize={44} // Estimated height of each row in pixels (default: 44)
      overscan={10} // Number of items to render outside the visible area (default: 5)
    />
  );
}
```

#### Performance Guidelines

- **Row Height Considerations**: Ensure consistent row heights. Avoid variable content that changes row height.

  ```tsx
  // ✅ Good: Fixed row heights
  const columns = [
    {
      accessorKey: "name",
      header: "Name",
      size: 200,
      maxSize: 200, // Prevents layout shifts
    },
  ];

  // ❌ Avoid: Variable content that changes row height
  const columns = [
    {
      accessorKey: "description",
      header: "Description",
      cell: ({ getValue }) => <div style={{ height: Math.random() * 100 }}>{getValue()}</div>,
    },
  ];
  ```

- **Optimal Configuration**: Start with `overscan={5}` and adjust if you see blank areas during fast scrolling. Ensure `estimateRowSize` matches your actual row height.

#### Troubleshooting Virtualization Issues

- **Blank Areas During Scrolling**: Increase `overscan` (e.g., to 10-20) or adjust `estimateRowSize` to match actual row height.
- **Poor Performance**: Reduce `overscan`, optimize cell components, and use `React.memo` for complex cell renderers.
- **Layout Shifts**: Ensure all rows have the same height and set fixed column widths.
- **Scrolling Issues**: Ensure `tableHeight` is set and the table container has fixed dimensions.

### 4.4 Row Actions

The `DataTable` component allows you to define custom actions for each row using the `renderRowActions` prop. This is useful for implementing context-specific actions like

editing, viewing, or deleting a row.

```typescript
// components/DataTableRowActions.tsx
import React from "react";
import { Row } from "gends";
// Assuming these icons and components are available from GENDS or your UI library
import { IcVisible, IcEdit, IcMoreHorizontal, IcCopy, IcTrash } from "gends";
import { Button } from "gends";
import {
  DropdownMenu,
  DropdownMenuTrigger,
  DropdownMenuContent,
  DropdownMenuItem,
} from "gends";
import Tooltip from "gends";

export function DataTableRowActions<TData>({ row }: { row: Row<TData> }) {
  return (
    <div className="flex items-center space-x-1">
      <Tooltip content="View">
        <Button
          variant="ghost"
          size="sm"
          onClick={() => console.log("View", row.original)}
        >
          <IcVisible className="h-4 w-4" />
        </Button>
      </Tooltip>

      <Tooltip content="Edit">
        <Button
          variant="ghost"
          size="sm"
          onClick={() => console.log("Edit", row.original)}
        >
          <IcEdit className="h-4 w-4" />
        </Button>
      </Tooltip>

      <DropdownMenu>
        <DropdownMenuTrigger asChild>
          <Button variant="ghost" size="sm">
            <IcMoreHorizontal className="h-4 w-4" />
          </Button>
        </DropdownMenuTrigger>
        <DropdownMenuContent side="left">
          <DropdownMenuItem onClick={() => console.log("Duplicate", row)}>
            <IcCopy className="mr-2 h-4 w-4" />
            Duplicate
          </DropdownMenuItem>
          <DropdownMenuItem
            onClick={() => console.log("Delete", row)}
            className="text-destructive"
          >
            <IcTrash className="mr-2 h-4 w-4" />
            Delete
          </DropdownMenuItem>
        </DropdownMenuContent>
      </DropdownMenu>
    </div>
  );
}
```

To integrate this into your `DataTable`:

```typescript
import { DataTable } from "gends";
import { DataTableRowActions } from "gends";
// ... inside your component where you render DataTable

<DataTable
  table={table}
  // ... other props
  renderRowActions={(row) => <DataTableRowActions row={row} />}
/>;
```

**Explanation:**

- **`renderRowActions` Prop**: This prop accepts a function that receives the `row` object from `@tanstack/react-table` and should return a `React.ReactNode`. This allows you to create highly customized action components for each row.
- **`DataTableRowActions` Component**: This example component demonstrates how to create a set of buttons and a dropdown menu for common row actions (View, Edit, Duplicate, Delete). It uses GENDS UI components like `Button`, `Tooltip`, and `DropdownMenu`.

### 4.5 Customizing Headers and Footers

The `DataTable` provides flexible props to inject custom React nodes into various sections of the table header and footer, allowing for highly customized layouts and controls.

```typescript
<DataTable
  table={table}
  // ... other props
  headerTopRow={
    <div className="border-b bg-white px-4 py-2">
      {/* Your custom content for the very top of the header */}
      <p>Global Table Controls</p>
    </div>
  }
  showHeaderTopRow={true}
  headerMiddleRow={
    <div className="px-4 py-2">
      {/* Content for the middle section of the header, often used for search/filters */}
      {/* Example: <SearchInput /> */}
    </div>
  }
  showHeaderMiddleRow={true}
  headerBottomRow={
    <div className="px-4 py-2">
      {/* Content for the bottom section of the header, often used for filter pills or column managers */}
      {/* Example: <FilterPills table={table} /> */}
    </div>
  }
  showHeaderBottomRow={true}
  tableFooter={
    <div className="flex justify-between items-center px-4 py-2 border-t">
      {/* Custom content for the table footer, e.g., pagination, summary */}
      <span>Total Rows: {table.getRowCount()}</span>
      {/* <Pagination ... /> */}
    </div>
  }
  showTableFooter={true}
  stickyFooter={true} // Makes the footer stick to the bottom on scroll
/>
```

**Explanation:**

- **`headerTopRow`, `headerMiddleRow`, `headerBottomRow`**: These props accept any `React.ReactNode` and allow you to place custom components (like search bars, filter pills, or column managers) in distinct sections of the table header. The `showHeaderTopRow`, `showHeaderMiddleRow`, and `showHeaderBottomRow` boolean props control their visibility.
- **`tableFooter`**: Similar to the header props, this allows you to render custom content at the bottom of the table. It's commonly used for pagination controls or summary information. `showTableFooter` controls its visibility, and `stickyFooter` makes it stick to the bottom of the viewport during scrolling.

### 4.6 Loading States (Shimmer Effect)

To provide a better user experience during data fetching, the `DataTable` component supports a shimmer loading effect.

```typescript
<DataTable
  table={table}
  // ... other props
  isLoading={true} // Set to true when data is being fetched
  shimmerRowCount={7} // Number of shimmer rows to display (default is 5)
/>
```

**Explanation:**

- **`isLoading`**: When set to `true`, the table will display a shimmer animation over the rows, indicating that data is being loaded. This is typically controlled by your data fetching logic.
- **`shimmerRowCount`**: Specifies how many shimmer rows should be displayed. Adjust this based on the typical number of rows you expect to see.

### 4.7 Truncation and Wrapping

The `DataTable` provides fine-grained control over how cell content is displayed when it overflows, offering options for truncation with tooltips or text wrapping.

```typescript
<DataTable
  table={table}
  // ... other props
  truncateAll={true} // Truncate all columns by default (shows tooltip on hover)
  truncateColumns={["description", "notes"]} // Explicitly truncate these columns (overrides wrapAll/truncateAll if specified)
  wrapAll={false} // Do not wrap all columns by default
  wrapColumns={["address", "comments"]} // Explicitly wrap these columns
/>
```

**Explanation:**

- **`truncateAll`**: If `true` (default), all cell content will be truncated with an ellipsis if it overflows, and a tooltip will appear on hover to show the full content.
- **`truncateColumns`**: An array of column IDs. If a column's ID is in this list, its content will be truncated, overriding `wrapAll` or `truncateAll` for that specific column.
- **`wrapAll`**: If `true`, all cell content will wrap to multiple lines if it overflows.
- **`wrapColumns`**: An array of column IDs. If a column's ID is in this list, its content will wrap, overriding `truncateAll` or `wrapAll` for that specific column.

### 4.8 Sub-tables (Nested Data)

The `DataTable` supports displaying hierarchical data using sub-tables. You can either provide column definitions for a default sub-table renderer or supply your own custom sub-table component.

```typescript
import { DataTable, ColumnDef } from "gends";

interface ParentRow {
  id: number;
  name: string;
  // ... other parent data
  subRows?: ChildRow[]; // For expandable rows (nested data)
  subTableData?: OtherChildRow[]; // For a separate sub-table
}

interface ChildRow {
  childId: number;
  childName: string;
}

interface OtherChildRow {
  otherChildId: number;
  otherChildValue: string;
}

// Option 1: Using default sub-table renderer with subTableColumnDef
const subTableColumns: ColumnDef<OtherChildRow>[] = [
  { accessorKey: "otherChildId", header: "Sub-Table ID" },
  { accessorKey: "otherChildValue", header: "Sub-Table Value" },
];

<DataTable<ParentRow>
  table={table}
  // ... other props
  subRowKey="subRows" // Key for nested rows (for expandable rows)
  subTableKey="subTableData" // Key for data to be passed to SubTableComponent or subTableColumnDef
  subTableColumnDef={subTableColumns} // Column definitions for the default sub-table
/>;

// Option 2: Using a custom SubTableComponent
import { CustomASNTable } from "./custom-asn-table"; // Your custom component

<DataTable<ParentRow>
  table={table}
  // ... other props
  subRowKey="subRows"
  subTableKey="subTableData"
  SubTableComponent={({ data }) => (
    <CustomASNTable data={data as OtherChildRow[]} />
  )} // Your custom component
/>;
```

**Explanation:**

- **`subRowKey`**: Specifies the key in your data object that contains an array of nested rows. These nested rows will be displayed directly below the parent row when expanded.
- **`subTableKey`**: Specifies the key in your data object that contains data for a separate sub-table. This data will be passed to either the `SubTableComponent` or rendered using `subTableColumnDef`.
- **`subTableColumnDef`**: If you want to use the default sub-table rendering, provide an array of `ColumnDef` for the sub-table data.
- **`SubTableComponent`**: For more complex sub-table layouts, you can provide your own React component. This component will receive the sub-table `data` as a prop.

## 5. Edge Cases and Best Practices

### 5.1 Handling Empty States

When the table has no data to display, the `DataTable` component renders an empty state. You can customize the message and height of this empty state.

```typescript
<DataTable
  table={table}
  // ... other props
  emptyStateHeight="300px" // Customize the height of the empty state area
/>
```

By default, if `table.getRowModel().rows.length` is 0, an empty state message "No results." will be displayed. You can customize this message by providing a `message` prop to the `TableEmptyState` component if you are using it directly, or ensure your `table` instance correctly reflects an empty state.

### 5.2 Performance Considerations

- **Virtualization**: For large datasets (1,000+ rows), always enable `enableVirtualization` and provide an accurate `estimateRowSize` and appropriate `overscan` value.
- **Memoization**: For complex cell renderers or custom components passed as props (e.g., `headerTopRow`, `tableFooter`), use `React.memo` or `useCallback`/`useMemo` to prevent unnecessary re-renders.
- **Column Sizing**: Define `size`, `minSize`, and `maxSize` for your columns to prevent layout shifts and ensure consistent rendering, especially with virtualization.

### 5.3 Responsive Design

The `DataTable` component is designed to be responsive. Ensure that your custom content within headers, footers, and cells also adapts well to different screen sizes. Using CSS utilities like `flexbox` and `grid` with responsive breakpoints is recommended.

### 5.4 Accessibility

- **Semantic HTML**: The `DataTable` uses semantic HTML elements for tables. Ensure any custom content you inject also follows accessibility best practices.
- **Keyboard Navigation**: `@tanstack/react-table` provides good keyboard navigation out-of-the-box. Test your custom interactive elements (e.g., buttons in row actions, editable cells) for keyboard accessibility.
- **ARIA Attributes**: If you implement complex custom interactions, consider adding appropriate ARIA attributes to enhance accessibility for screen reader users.

### 5.5 Debugging

- **`console.warn` for missing table instance**: The component will log a warning to the console if it renders without a `table` instance. This is a common issue during initial setup or when data is asynchronously loaded.
- **React DevTools**: Use React DevTools to inspect the component tree, props, and state of the `DataTable` and its children to debug rendering issues.
- **TanStack Table DevTools**: `@tanstack/react-table` also offers a devtools extension that can be invaluable for understanding table state and debugging column/row models.

## 6. Conclusion

The `DataTable` component is a powerful and versatile tool for displaying and managing tabular data in your MCP server applications. By leveraging `@tanstack/react-table` and providing extensive customization options, it enables developers to create rich, interactive, and performant data tables tailored to specific application needs. Adhering to the best practices outlined in this document will help ensure optimal performance, maintainability, and user experience.

For further details on `@tanstack/react-table` capabilities, refer to its official documentation.
