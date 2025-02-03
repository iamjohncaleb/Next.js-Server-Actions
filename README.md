# 🚀 Next.js Server Actions Template  

This repository demonstrates the usage of **Next.js Server Actions**, a new feature in Next.js that enables seamless server-side logic execution directly from React components without needing API routes.  

---

## 📌 Features  

- ✅ **Simplified Server-Side Logic**: No need for API routes—call server functions directly from components.  
- 🔐 **Built-in Security**: Data processing happens on the server, reducing client-side vulnerabilities.  
- ⚡ **Optimized Performance**: Faster interactions with less client-side JavaScript.  
- 🔄 **Streaming & Mutations**: Handle form submissions and data mutations efficiently.  
- 📦 **Full-Stack in One Repo**: Next.js handles both frontend and backend logic in a unified setup.  

---

## 🛠 Tech Stack  

- **Framework**: [Next.js 14+](https://nextjs.org/)  
- **Language**: TypeScript (or JavaScript)  
- **Database**: PostgreSQL / MongoDB (optional)  
- **Authentication**: NextAuth.js or custom session handling (optional)  
- **Styling**: Tailwind CSS  

---

## 📦 Installation & Setup  

### **1. Clone the Repository**  
```bash
git clone https://github.com/yourusername/nextjs-server-actions.git
cd nextjs-server-actions
```

### **2. Install Dependencies**  
```bash
npm install
# or
yarn install
```

### **3. Set Up Environment Variables**  
Create a `.env.local` file in the root directory and add any required variables:  
```plaintext
DATABASE_URL=your_database_url
NEXTAUTH_SECRET=your_secret_key
```

### **4. Start the Development Server**  
```bash
npm run dev
# or
yarn dev
```
Visit [http://localhost:3000](http://localhost:3000) in your browser.  

---

## 📂 Folder Structure  
```plaintext
├── app                // Next.js app directory
│   ├── actions        // Server actions (handle form submissions, mutations)
│   ├── components     // UI components
│   ├── pages          // Pages and layouts
│   ├── styles         // Global styles
│   ├── lib            // Utility functions, database connections
│   ├── api            // (Optional) API routes
├── public             // Static assets
├── prisma             // (Optional) Database schema (for Prisma ORM)
└── README.md          // Project documentation
```

---

## ✅ Example Server Action  

Here’s a simple example of a server action that **submits a form** and saves data to a database:  

```tsx
"use server";

import { db } from "@/lib/db"; // Database connection

export async function createUser(data: FormData) {
  const name = data.get("name") as string;
  const email = data.get("email") as string;

  if (!name || !email) {
    throw new Error("Missing required fields");
  }

  await db.user.create({
    data: { name, email },
  });

  return { success: true };
}
```

**Usage in a Component:**  
```tsx
"use client";

import { useState } from "react";
import { createUser } from "../actions/createUser";

export default function SignUpForm() {
  const [message, setMessage] = useState("");

  async function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
    event.preventDefault();
    const formData = new FormData(event.currentTarget);
    const response = await createUser(formData);
    
    setMessage(response.success ? "User created!" : "Error occurred.");
  }

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" type="text" placeholder="Name" required />
      <input name="email" type="email" placeholder="Email" required />
      <button type="submit">Submit</button>
      {message && <p>{message}</p>}
    </form>
  );
}
```

---

## 🔗 Deployment  

- **Hosting**: [Vercel](https://vercel.com/) (Recommended)  
- **Database**: Supabase / Prisma with PostgreSQL  
- **Environment Variables**: Add `.env` variables in the deployment dashboard  

---

## 👥 Contributing  

1. Fork the repository.  
2. Create a new feature branch (`git checkout -b feature-branch`).  
3. Commit your changes (`git commit -m "Added new feature"`).  
4. Push to your branch (`git push origin feature-branch`).  
5. Submit a pull request.  

---

## 📜 License  

This project is licensed under the **MIT License**.  

---

## 📞 Contact  

- **Author**: Daniella Obiagwuna  
- **Email**: [your-email@example.com](mailto:your-email@example.com)  
- **GitHub**: [your-github-profile](https://github.com/yourusername)  
- **LinkedIn**: [Your LinkedIn Profile](https://linkedin.com/in/yourprofile)  

---

Let me know if you’d like any modifications or additional details! 😊🚀