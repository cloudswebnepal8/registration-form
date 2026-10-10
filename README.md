# Student Registration Form

A single-page student registration form built with **React** and **Vite**, using plain CSS for styling. The form demonstrates controlled components, client-side validation, and a custom success modal.

## Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Start the development server:

   ```bash
   npm run dev
   ```

3. Open the URL shown in the terminal (usually `http://localhost:5173`).

## Build for production

```bash
npm run build
npm run preview
```

## Project structure

```
src/
├── App.jsx                      # Top-level layout (sunset background + form)
├── components/
│   ├── RegistrationForm.jsx     # Form state, validation, and submit logic
│   ├── RegistrationForm.css
│   ├── SuccessModal.jsx         # Success popup with submitted data summary
│   └── SuccessModal.css
└── main.jsx
```

## How form state works

All form fields are stored in a **single `formData` object** managed by one `useState` hook:

```js
const [formData, setFormData] = useState({
  fullName: '',
  address: '',
  email: '',
  phone: '',
  course: '',
  gender: '',
  dateOfBirth: '',
})
```

This is the **controlled component** pattern: each input's `value` is bound to `formData`, and `onChange` calls a shared `handleChange` function that updates the matching field. React always controls what appears in the inputs, which makes validation and reset logic straightforward.

When the user edits a field that currently has an error, that field's error is cleared immediately so feedback feels responsive.

## How validation works

Validation runs **on submit** (not via the browser's native popups — the form uses `noValidate`). A separate `errors` object tracks which fields failed:

- **Required fields** — all fields must be filled.
- **Email** — checked with a regex (`/^[^\s@]+@[^\s@]+\.[^\s@]+$/`).
- **Phone** — non-digit characters are stripped, then the digit count must be between 7 and 15.

If validation fails, red inline messages appear below the relevant fields. If it passes, a custom **SuccessModal** shows a summary of the submitted data. Clicking **OK** closes the modal and resets the form.

The **Cancel** button asks for confirmation (via `window.confirm`) before clearing all fields.
