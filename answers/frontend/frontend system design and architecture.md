### **Frontend System Design & Architecture - Answers**

---

## **1. Application Architecture**

### **What are the different frontend architectures, and when should you use each?**

Frontend architectures define how the UI layer of an application is structured. The most common types are:

- **Monolithic Architecture** – Traditional architecture where the frontend is tightly coupled with the backend.

  - Best for: Small-to-medium applications, single-page applications (SPAs).

- **Microfrontend Architecture** – The frontend is broken into independent modules, developed and deployed separately.

  - Best for: Large-scale applications with multiple teams working independently.

- **Server-Side Rendering (SSR)** – HTML is generated on the server for each request.

  - Best for: SEO-heavy applications, pages that require fast initial load times (e.g., blogs, e-commerce).

- **Client-Side Rendering (CSR)** – The browser downloads a JS bundle and renders the UI dynamically.

  - Best for: Interactive web apps (e.g., dashboards, social media apps).

- **Static Site Generation (SSG)** – Pages are pre-rendered at build time.
  - Best for: Blogs, documentation sites (e.g., Next.js with `getStaticProps`).

---

### **Monolith vs. Microfrontend Architecture – Pros and Cons**

| Feature         | Monolith                      | Microfrontend                  |
| --------------- | ----------------------------- | ------------------------------ |
| **Scalability** | Harder to scale independently | Scales well across teams       |
| **Deployment**  | Full deployment required      | Independent deployment         |
| **Complexity**  | Easier for small apps         | More complex infrastructure    |
| **Performance** | Usually faster for small apps | May introduce overhead         |
| **Best for**    | Small-medium apps             | Large apps with multiple teams |

---

### **Client-side Rendering (CSR) vs. Server-side Rendering (SSR) vs. Static Site Generation (SSG)**

| Feature           | CSR (React SPA)      | SSR (Next.js)       | SSG (Next.js)        |
| ----------------- | -------------------- | ------------------- | -------------------- |
| **Performance**   | Slower initial load  | Faster initial load | Fastest initial load |
| **SEO**           | Poor                 | Good                | Best                 |
| **Data Fetching** | Fetch on client-side | Fetch per request   | Fetch at build time  |
| **Use Case**      | Web apps, dashboards | Blogs, e-commerce   | Blogs, landing pages |

---

### **How does Next.js improve performance compared to traditional React apps?**

- **Hybrid rendering** – Supports CSR, SSR, and SSG.
- **Automatic code-splitting** – Reduces JS bundle size.
- **Image Optimization** – Uses `<Image>` component for optimized image delivery.
- **Static Site Generation (SSG)** – Pre-renders pages at build time for better performance.

---

### **What are Isomorphic (Universal) Applications, and how do they work?**

Isomorphic apps run the same JavaScript code on both the **server** and **client**. Initially, content is rendered on the server, then hydrated on the client for interactivity. Next.js is a great example.

**Example:**

```javascript
export async function getServerSideProps() {
  const res = await fetch("https://api.example.com");
  const data = await res.json();
  return { props: { data } };
}
```

---

### **How does the Backend-for-Frontend (BFF) pattern improve frontend development?**

BFF is a layer between the frontend and backend that provides a tailored API for frontend needs.

**Benefits:**

- Reduces over-fetching of data.
- Improves performance and security.
- Simplifies frontend logic.

**Example:** Instead of querying multiple microservices, the frontend calls a BFF that aggregates data from different APIs.

---

## **2. State Management**

### **What are the different state types in a frontend application?**

1. **Local State** – UI state within a component (`useState` in React).
2. **Global State** – Shared state across components (`useContext`, Redux).
3. **Server State** – External data fetched from APIs (`React Query`).
4. **UI State** – Temporary states like modal visibility.

---

### **When to use Redux, Recoil, Zustand, or Context API?**

| Library         | Best for                                       |
| --------------- | ---------------------------------------------- |
| **Redux**       | Complex global state management                |
| **Recoil**      | Simpler alternative to Redux with atomic state |
| **Zustand**     | Lightweight, easy-to-use state management      |
| **Context API** | Small-scale state sharing                      |

---

### **What is Optimistic vs. Pessimistic UI updates?**

- **Optimistic UI** – Assume success and update the UI before the API response.
- **Pessimistic UI** – Wait for API confirmation before updating the UI.

**Example (Optimistic UI in React Query):**

```javascript
const mutation = useMutation(updatePost, {
  onMutate: async (newData) => {
    queryClient.setQueryData("posts", (old) => [...old, newData]);
  },
});
```

---

## **3. Performance Optimization**

### **How do you optimize a React application for better performance?**

- **Use React.memo** to avoid unnecessary re-renders.
- **Lazy load components** using `React.lazy`.
- **Minimize re-renders** with `useMemo` and `useCallback`.
- **Reduce bundle size** using tree shaking and code splitting.

---

### **What is code splitting, and how does it reduce bundle size?**

Code splitting breaks JS bundles into smaller parts that load dynamically, reducing initial page load time.

**Example:**

```javascript
const Dashboard = React.lazy(() => import("./Dashboard"));
<Suspense fallback={<Loader />}>
  <Dashboard />
</Suspense>;
```

---

## **4. Scalability & Maintainability**

### **How do you structure a frontend codebase for scalability?**

- **Feature-based structure** (`components`, `pages`, `hooks`, `store`).
- **Atomic design principles** – Break UI into atoms, molecules, organisms.
- **Separate concerns** – Keep logic separate from UI components.

---

## **5. API Design & Data Fetching**

### **What are different API fetching patterns in frontend applications?**

- **REST API** – Standard CRUD operations (`fetch`, `axios`).
- **GraphQL** – Flexible querying for fetching only required data.
- **Polling** – Repeated requests for updated data.
- **WebSockets** – Real-time bidirectional communication.

---

### **How do you handle caching in API requests?**

- **React Query/SWR** – Cache and update stale data efficiently.
- **Local Storage/sessionStorage** – Cache non-sensitive data.

---

## **6. Security & Authentication**

### **What are CORS and CSRF attacks, and how do you prevent them?**

- **CORS (Cross-Origin Resource Sharing)** – Prevents unauthorized cross-origin requests.
  - Solution: Use proper `Access-Control-Allow-Origin` headers.
- **CSRF (Cross-Site Request Forgery)** – Forces users to perform unintended actions.
  - Solution: Use CSRF tokens and `SameSite` cookies.

---

### **How does OAuth, JWT, and session-based authentication work?**

| Method      | How it Works                                     |
| ----------- | ------------------------------------------------ |
| **OAuth**   | Secure third-party authentication (Google Login) |
| **JWT**     | Token-based authentication for APIs              |
| **Session** | Stores session data on the server                |

---

## **7. Error Handling & Logging**

### **How do you handle errors gracefully in a frontend application?**

- Use **try/catch** for API requests.
- Implement **error boundaries** in React.
- Use **logging tools** (Sentry, LogRocket).

**Example:**

```javascript
class ErrorBoundary extends React.Component {
  componentDidCatch(error, info) {
    console.log(error, info);
  }
  render() {
    return this.props.children;
  }
}
```

---

## **8. Frontend Deployment & CI/CD**

### **What are the best strategies for frontend deployment?**

- **Netlify, Vercel** – Fast CI/CD for frontend apps.
- **Docker/Kubernetes** – Containerized deployments for scalability.
- **Blue-Green Deployment** – Avoids downtime by switching between two environments.

---
