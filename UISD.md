# User Management Screen Specification

## Overview

The User Management screen is used by administrators to manage system users.

Administrators should be able to:

- View users
- Create a new user
- Edit an existing user
- Enable or disable a user
- Assign roles to a user
- Sort and filter the user table
- Use the screen in both light mode and dark mode

The page has two main parts:

| Area | Description |
| --- | --- |
| User List | Shows existing users in a table. |
| User Form | Used to create or edit a user. |

## Initial Page State

When the page opens:

- The user table is shown on the left.
- The user form is shown on the right.
- The form is in **New User** mode.
- All form fields are empty.
- **Hide Disabled User** is checked by default.
- Only enabled users are shown in the table.
- **+ New User** is shown at the top-left.
- **Save User** is shown at the top-right.

## Layout

The page should have a toolbar at the top and two columns below it.

| Section | Position | Width |
| --- | --- | --- |
| Toolbar | Top | Full width |
| User List | Left | 50% |
| User Form | Right | 50% |

## Toolbar

### + New User Button

When the administrator clicks **+ New User**:

- The form title becomes **New User**.
- All fields are cleared.
- No table row is selected.
- The form switches to create mode.
- Clicking **Save User** creates a new user.

### Hide Disabled User Checkbox

Default value: checked.

When checked:

- Disabled users are hidden from the table.

When unchecked:

- Enabled and disabled users are both shown.

The table should update immediately when this checkbox changes.

### Save User Button

When clicked:

- The form is validated.
- If the form is valid and the form is in create mode, a new user is created.
- If the form is valid and the form is in edit mode, the selected user is updated.
- If the form is invalid, error messages are shown near the invalid fields.

## User Table

The user table displays existing users.

### Columns

| Column | Description | Example |
| --- | --- | --- |
| ID | Unique user ID | `1` |
| User Name | Login name | `AdminUser` |
| Email | User email | `admin@piworks.net` |
| Enabled | User status | `true` |

### Example Data

| ID | User Name | Email | Enabled |
| --- | --- | --- | --- |
| 1 | AdminUser | admin@piworks.net | true |
| 2 | Test User | testuser@piworks.net | true |

### Row Selection

When the administrator clicks a user row:

- The row is highlighted.
- The form switches to **Edit User** mode.
- The selected user's data is loaded into the form.
- Clicking **Save User** updates that user.

### Sorting

Each table column should be sortable.

Clicking a column header should work like this:

1. First click: sort ascending
2. Second click: sort descending
3. Third click: remove sorting, if supported

Sortable columns:

- ID
- User Name
- Email
- Enabled

### Filtering

Each table column should support filtering.

Suggested filters:

| Column | Filter Type |
| --- | --- |
| ID | Number filter |
| User Name | Text filter |
| Email | Text filter |
| Enabled | Boolean filter |

## User Form

The form is used for both creating and editing users.

| Mode | Form Title |
| --- | --- |
| Create | New User |
| Edit | Edit User |

## Form Fields

### Username

| Property | Value |
| --- | --- |
| Type | Text input |
| Required | Yes |
| Max Length | 50 characters |

Rules:

- Cannot be empty.
- Must be unique.
- Cannot start or end with spaces.

Error messages:

- Username is required.
- Username already exists.
- Username cannot exceed 50 characters.

### Display Name

| Property | Value |
| --- | --- |
| Type | Text input |
| Required | Yes |
| Max Length | 100 characters |

Rules:

- Cannot be empty.
- Cannot exceed 100 characters.

Error messages:

- Display name is required.
- Display name cannot exceed 100 characters.

### Phone

| Property | Value |
| --- | --- |
| Type | Text input |
| Required | No |
| Max Length | 20 characters |

Rules:

- Can be empty.
- If entered, must be a valid phone number.
- Cannot exceed 20 characters.

Error messages:

- Phone number is not valid.
- Phone number cannot exceed 20 characters.

### Email

| Property | Value |
| --- | --- |
| Type | Email input |
| Required | Yes |
| Max Length | 100 characters |

Rules:

- Cannot be empty.
- Must be a valid email address.
- Must be unique.
- Cannot exceed 100 characters.

Error messages:

- Email is required.
- Email address is not valid.
- Email already exists.
- Email cannot exceed 100 characters.

### User Roles

| Property | Value |
| --- | --- |
| Type | Multi-select dropdown |
| Required | Yes |
| Placeholder | Select user roles... |

Available roles:

- Guest
- Admin
- SuperAdmin

Rules:

- The administrator can select one or more roles.
- At least one role must be selected.

Error message:

- At least one user role must be selected.

### Enabled

| Property | Value |
| --- | --- |
| Type | Checkbox |
| Required | No |

When checked:

- The user is active.

When unchecked:

- The user is disabled.

If **Hide Disabled User** is checked, disabled users should not appear in the table.

## Dark Mode

The screen must support dark mode.

Requirements:

- The screen should follow the system or application theme.
- Dark mode should apply to the whole page, including the toolbar, table, form, inputs, dropdowns, buttons, messages, and validation errors.
- Switching between light mode and dark mode should not clear form data.
- Switching themes should not reset selected rows, sorting, filtering, or validation messages.
- Text must be readable in dark mode.
- Buttons, checkboxes, inputs, and selected rows must be clearly visible.
- Error and success messages must be easy to read in dark mode.
- Keyboard focus indicators must be visible in dark mode.

## Create User Flow

1. Click **+ New User**.
2. Fill in the form.
3. Select at least one role.
4. Optionally check **Enabled**.
5. Click **Save User**.
6. Validate the form.
7. If valid, create the user.
8. Refresh the table.
9. Show this success message:

```text
User has been created successfully.
```

## Edit User Flow

1. Click a user row in the table.
2. Load the selected user's data into the form.
3. Edit the needed fields.
4. Click **Save User**.
5. Validate the form.
6. If valid, update the user.
7. Refresh the table.
8. Show this success message:

```text
User has been updated successfully.
```

## Validation

Validation should happen when:

- The administrator clicks **Save User**.
- A required field is empty.
- Email format is invalid.
- Phone format is invalid.
- No user role is selected.

Invalid fields should be highlighted, and each error message should be shown close to its field.

## Error Messages

| Case | Message |
| --- | --- |
| Save failed | User could not be saved. Please try again. |
| Server error | An unexpected error occurred. Please contact the system administrator. |
| Duplicate username | Username already exists. |
| Duplicate email | Email already exists. |

## Empty Table Messages

If there are no users:

```text
No users found.
```

If **Hide Disabled User** is checked and all users are disabled:

```text
No enabled users found.
```

## Accessibility

The page should be usable by keyboard and screen readers.

Requirements:

- Every input must have a visible label.
- Buttons, checkboxes, inputs, and dropdowns must be reachable with the Tab key.
- Dropdown options must be selectable using the keyboard.
- Error messages must be readable by screen readers.
- Color must not be the only way to show errors.
- Light mode and dark mode must both have readable contrast.

## Acceptance Criteria

The screen is complete when:

- Existing users are shown in the table.
- Disabled users can be hidden or shown.
- A new user can be created.
- An existing user can be selected and edited.
- Required fields are validated.
- Username and email uniqueness are checked.
- At least one user role is required.
- The table refreshes after create and update actions.
- Success and error messages are shown correctly.
- Sorting works in the table.
- Filtering works in the table.
- Light mode and dark mode both work.
- Switching themes does not reset page data.
- The page can be used with keyboard navigation.
