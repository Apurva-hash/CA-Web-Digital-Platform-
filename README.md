
\documentclass[12pt,a4paper]{article}

\usepackage[margin=1in]{geometry}
\usepackage{xcolor}
\usepackage{hyperref}
\usepackage{enumitem}
\usepackage{titlesec}
\usepackage{listings}
\usepackage{parskip}

\definecolor{primary}{RGB}{35,75,130}
\definecolor{codebg}{RGB}{245,247,250}

\hypersetup{
    colorlinks=true,
    linkcolor=primary,
    urlcolor=blue,
    pdftitle={CA Web Platform Documentation}
}

\titleformat{\section}
  {\Large\bfseries\color{primary}}
  {\thesection}{1em}{}

\lstset{
    basicstyle=\ttfamily\small,
    backgroundcolor=\color{codebg},
    frame=single,
    breaklines=true,
    columns=fullflexible
}

\title{
    \textbf{\Huge CA Web Platform}\\[0.5cm]
    \large Project Documentation
}
\author{Apurva Hippargi}
\date{\today}

\begin{document}

\maketitle
\tableofcontents
\newpage

\section{Project Overview}

The CA Web Platform is a web-based application designed
to connect clients with Chartered Accountants (CAs).
It helps manage accounting-service workflows through
separate client and CA portals.

The platform supports service requests, document
management, communication, and task tracking in one place.

\section{Features}

\subsection{Public Access}
\begin{itemize}
    \item Landing page introducing the platform.
    \item User registration and login.
    \item Role-based routing for clients and CA accounts.
\end{itemize}

\subsection{Client Portal}
\begin{itemize}
    \item Client dashboard.
    \item Find a Chartered Accountant.
    \item Submit service requests and track their status.
    \item Upload and view documents.
    \item Access messages and conversations.
    \item Manage user profiles.
\end{itemize}

\subsection{CA Portal}
\begin{itemize}
    \item Dashboard with overview statistics and charts.
    \item Client management.
    \item Service-request management.
    \item Document management.
    \item Task management.
    \item Messaging and account settings.
\end{itemize}

\subsection{Backend Services}
\begin{itemize}
    \item REST API built with Express.
    \item JWT-protected routes.
    \item MongoDB persistence using Mongoose.
    \item Password hashing with bcryptjs.
    \item Financial and regulatory news aggregation.
    \item Stripe-configured payment routes.
    \item AWS S3 and Cloudinary document-storage integrations.
    \item Helmet security middleware and API rate limiting.
\end{itemize}

\section{Technology Stack}

\subsection{Frontend}
\begin{itemize}
    \item React 19
    \item TypeScript
    \item Vite
    \item React Router
    \item Recharts
    \item Framer Motion
    \item Lucide React
    \item CSS
\end{itemize}

\subsection{Backend}
\begin{itemize}
    \item Node.js
    \item Express.js
    \item MongoDB and Mongoose
    \item JSON Web Tokens (JWT)
    \item bcryptjs
    \item rss-parser
    \item Stripe SDK
    \item AWS SDK for S3
    \item Cloudinary
    \item Helmet and express-rate-limit
\end{itemize}

\section{Project Structure}

\begin{lstlisting}
CA web pro/
|-- frontend/
|   |-- src/
|   |   |-- components/
|   |   |-- context/
|   |   |-- pages/
|   |   |   |-- ca/
|   |   |   |-- user/
|   |   |-- config/
|   |   |-- App.tsx
|   |-- public/
|   |-- package.json
|   |-- vite.config.ts
|
|-- backend/
    |-- config/
    |-- controllers/
    |-- middleware/
    |-- models/
    |-- routes/
    |-- index.js
    |-- package.json
\end{lstlisting}

\section{Prerequisites}

Before running the application, install:
\begin{itemize}
    \item Node.js and npm.
    \item A MongoDB database.
    \item Credentials for external services you want to enable,
    such as AWS S3, Stripe, or Cloudinary.
\end{itemize}

\section{Installation and Setup}

Run the frontend and backend in separate terminals.

\subsection{Backend Setup}

Navigate to the backend directory:

\begin{lstlisting}
cd "CA web pro/backend"
npm install
\end{lstlisting}

Create a \texttt{.env} file in the backend directory:

\begin{lstlisting}
PORT=5001
JWT_SECRET=replace_with_a_long_random_secret
MONGODB_URI=mongodb_connection_string

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
AWS_S3_BUCKET=

STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=

CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=
\end{lstlisting}

Start the backend:

\begin{lstlisting}
npm run dev
\end{lstlisting}

The backend defaults to port 5001 unless another port
is configured.

\subsection{Frontend Setup}

Open a second terminal:

\begin{lstlisting}
cd "CA web pro/frontend"
npm install
\end{lstlisting}

Create a frontend \texttt{.env} file if needed:

\begin{lstlisting}
VITE_API_URL=http://localhost:5001
\end{lstlisting}

Start the frontend:

\begin{lstlisting}
npm run dev
\end{lstlisting}

Vite will display the local development URL in the terminal.

\section{Build and Code Checks}

Run these commands from the frontend directory:

\begin{lstlisting}
npm run build
npm run lint
\end{lstlisting}

To preview the production build locally:

\begin{lstlisting}
npm run preview
\end{lstlisting}

\section{API Overview}

The backend mounts its API routes under \texttt{/api}.

\begin{itemize}
    \item \texttt{/api/auth}: Registration and authentication.
    \item \texttt{/api/ca}: CA-related operations.
    \item \texttt{/api/dashboard}: Dashboard statistics.
    \item \texttt{/api/documents}: Document operations.
    \item \texttt{/api/news}: Financial and regulatory news.
    \item \texttt{/api/requests}: Service requests.
    \item \texttt{/api/clients}: Client management.
    \item \texttt{/api/chat}: Messaging.
    \item \texttt{/api/payments}: Payment-related operations.
\end{itemize}

Most account-specific endpoints require a valid bearer token.

\section{Security Considerations}

\begin{itemize}
    \item Never commit \texttt{.env} files or API secrets
    to a public repository.
    \item Use a strong and private JWT secret.
    \item Configure CORS for trusted origins.
    \item Test payment integrations and webhooks before
    using real customer data or payments.
    \item Dashboard statistics include sample values and
    should not be treated as live business metrics.
\end{itemize}

\section{Deployment Notes}

The project contains a React/TypeScript frontend and a
Node.js/Express backend.

GitHub Pages can host the static frontend, but it cannot
run the Express backend or MongoDB database. Deploy those
services separately and configure the frontend API URL
to point to the hosted backend.

External integrations require valid credentials and
appropriate environment configuration.

\section{Conclusion}

The CA Web Platform brings client and Chartered Accountant
workflows into one application. It provides a foundation
for managing service requests, documents, communication,
and tasks. Complete configuration and testing are required
before production use.

\section{License}

No project-specific license was identified in the
available project documentation. Add a LICENSE file
if you intend to distribute the project publicly.

\end{document}
