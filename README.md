
# DentIQ
=======
This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.



============================================
==============================================
================================================

# DentIQ - Complete Step-by-Step Guide to Build from Scratch

## Project Overview

**DentIQ** is an AI-powered dental assistant application built with Next.js 15. It features:
- **Appointment booking system** for dental consultations
- **AI voice assistant** (Vapi) for dental advice
- **User authentication** via Clerk
- **Email notifications** via Resend
- **Admin dashboard** for doctor management
- **Modern UI** with shadcn/ui components

## Tech Stack

- **Framework**: Next.js 15.5.0 (App Router)
- **Language**: TypeScript
- **Authentication**: Clerk
- **Database**: PostgreSQL with Prisma ORM
- **Voice AI**: Vapi AI
- **Email**: Resend
- **Styling**: Tailwind CSS v4
- **UI Components**: shadcn/ui (Radix UI)
- **State Management**: TanStack Query
- **Forms**: React Hook Form + Zod validation
- **Icons**: Lucide React
- **Code Quality**: Biome (linter/formatter)

---

## Step 1: Required Services & Account Setup

### 1. Clerk (Authentication)
- **Website**: https://clerk.com
- **Purpose**: User authentication and user management
- **Setup Steps**:
  1. Create a free account at clerk.com
  2. Create a new application
  3. Copy your API keys from the dashboard
  4. Enable "Email + Password" sign-up method
  5. Configure your allowed redirect URLs (http://localhost:3000 for development)

### 2. PostgreSQL Database
- **Options**: 
  - **Supabase** (recommended, free tier): https://supabase.com
  - **Neon** (free tier): https://neon.tech
  - **Railway**: https://railway.app
- **Setup Steps** (using Supabase):
  1. Create a free account at supabase.com
  2. Create a new project
  3. Go to Project Settings > Database
  4. Copy your connection string (URI format)
  5. Note: The connection string will be your DATABASE_URL

### 3. Vapi AI (Voice Assistant)
- **Website**: https://vapi.ai
- **Purpose**: AI voice assistant for dental advice
- **Setup Steps**:
  1. Create an account at vapi.ai
  2. Get your API key from the dashboard
  3. Create an assistant or use their default
  4. Copy your public API key (starts with `pk_`)

### 4. Resend (Email Service)
- **Website**: https://resend.com
- **Purpose**: Send appointment confirmation emails
- **Setup Steps**:
  1. Create a free account at resend.com
  2. Verify your email domain (or use the default resend.dev domain for testing)
  3. Copy your API key from the dashboard

---

## Step 2: Environment Variables Setup

Create a [.env](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/.env:0:0-0:0) file in your project root with the following variables:

```env
# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_your_clerk_publishable_key
CLERK_SECRET_KEY=sk_test_your_clerk_secret_key
CLERK_SIGN_IN_URL=/sign-in
CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_SIGN_IN_FORCE_REDIRECT_URL=/dashboard
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/dashboard
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/dashboard

# Database (PostgreSQL)
DATABASE_URL="postgresql://user:password@host:port/database?schema=public"

# Vapi AI (Voice Assistant)
NEXT_PUBLIC_VAPI_API_KEY=pk_your_vapi_public_key

# Resend (Email)
RESEND_API_KEY=re_your_resend_api_key

# App URL (for production)
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

**Note**: Replace all placeholder values with your actual API keys from the services you set up in Step 1.

---

## Step 3: Project Initialization

### 3.1 Create Next.js Project

```bash
# Create new Next.js project with TypeScript
npx create-next-app@latest dentiq --typescript --tailwind --eslint

# Navigate into project
cd dentiq

# Install additional dependencies
npm install @clerk/nextjs @prisma/client @radix-ui/react-accordion @radix-ui/react-alert-dialog @radix-ui/react-aspect-ratio @radix-ui/react-avatar @radix-ui/react-checkbox @radix-ui/react-collapsible @radix-ui/react-context-menu @radix-ui/react-dialog @radix-ui/react-dropdown-menu @radix-ui/react-hover-card @radix-ui/react-label @radix-ui/react-menubar @radix-ui/react-navigation-menu @radix-ui/react-popover @radix-ui/react-progress @radix-ui/react-radio-group @radix-ui/react-scroll-area @radix-ui/react-select @radix-ui/react-separator @radix-ui/react-slider @radix-ui/react-slot @radix-ui/react-switch @radix-ui/react-tabs @radix-ui/react-toggle @radix-ui/react-toggle-group @radix-ui/react-tooltip @react-email/components @react-email/render @tanstack/react-query @vapi-ai/web class-variance-authority clsx cmdk date-fns embla-carousel-react input-otp lucide-react next-themes prisma react-day-picker react-hook-form react-resizable-panels recharts resend sonner tailwind-merge vaul zod

# Install dev dependencies
npm install -D @biomejs/biome @tailwindcss/postcss @types/node @types/react @types/react-dom tailwindcss tw-animate-css typescript
```

### 3.2 Initialize shadcn/ui

```bash
npx shadcn@latest init
```

When prompted, select:
- Style: `new-york`
- Base color: `neutral`
- CSS variables: `yes`

### 3.3 Install Required shadcn/ui Components

```bash
npx shadcn@latest add button card input label select dialog dropdown-menu avatar badge calendar checkbox separator sheet tabs accordion alert-dialog switch slider scroll-area popover tooltip command
```

### 3.4 Configure Next.js

Update [next.config.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/next.config.ts:0:0-0:0):

```typescript
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "images.unsplash.com",
      },
      {
        protocol: "https",
        hostname: "avatar.iran.liara.run",
      },
      {
        protocol: "https",
        hostname: "img.clerk.com",
      },
    ],
    unoptimized: true,
  },
};

export default nextConfig;
```

---

## Step 4: Database Setup with Prisma

### 4.1 Initialize Prisma

```bash
npx prisma init
```

### 4.2 Configure Prisma Schema

Replace the content of [prisma/schema.prisma](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/prisma/schema.prisma:0:0-0:0) with:

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        String   @id @default(cuid())
  clerkId   String   @unique
  email     String   @unique
  firstName String?
  lastName  String?
  phone     String?
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  appointments Appointment[]

  @@map("users")
}

model Doctor {
  id          String   @id @default(cuid())
  name        String
  email       String   @unique
  phone       String
  speciality  String
  bio         String?
  imageUrl    String
  gender      Gender
  isActive    Boolean  @default(true)
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  appointments Appointment[]

  @@map("doctors")
}

model Appointment {
  id         String             @id @default(cuid())
  date       DateTime
  time       String
  duration   Int                @default(30)
  status     AppointmentStatus @default(CONFIRMED)
  notes      String?
  reason     String?
  createdAt  DateTime           @default(now())
  updatedAt  DateTime           @updatedAt

  userId     String
  doctorId   String

  user   User   @relation(fields: [userId], references: [id], onDelete: Cascade)
  doctor Doctor @relation(fields: [doctorId], references: [id], onDelete: Cascade)

  @@map("appointments")
}

enum Gender {
  MALE
  FEMALE
}

enum AppointmentStatus {
  CONFIRMED
  COMPLETED
}
```

### 4.3 Generate Prisma Client

```bash
npx prisma generate
```

### 4.4 Push Schema to Database

```bash
npx prisma db push
```

### 4.5 Create Prisma Client Instance

Create [src/lib/prisma.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/lib/prisma.ts:0:0-0:0):

```typescript
import { PrismaClient } from "@prisma/client";

const globalForPrisma = globalThis as unknown as {
  prisma: PrismaClient | undefined;
};

export const prisma =
  globalForPrisma.prisma ?? new PrismaClient();

if (process.env.NODE_ENV !== "production") globalForPrisma.prisma = prisma;
```

---

## Step 5: Clerk Authentication Setup

### 5.1 Install Clerk Middleware

Create [src/middleware.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/middleware.ts:0:0-0:0):

```typescript
import { clerkMiddleware } from '@clerk/nextjs/server';

export default clerkMiddleware();

export const config = {
  matcher: [
    '/((?!_next|[^?]*\\.(?:html?|css|js(?!on)|jpe?g|webp|png|gif|svg|ttf|woff2?|ico|csv|docx?|xlsx?|zip|webmanifest)).*)',
    '/(api|trpc)(.*)',
  ],
};
```

### 5.2 Configure Clerk Provider

Update [src/app/layout.tsx](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/app/layout.tsx:0:0-0:0):

```typescript
import type { Metadata } from "next";
import { Geist, Geist_Mono } from "next/font/google";
import "./globals.css";
import { ClerkProvider } from '@clerk/nextjs';
import UserSync from "@/components/UserSync";
import TanStackProvider from "@/components/providers/TanStackProviders";

const geistSans = Geist({
  variable: "--font-geist-sans",
  subsets: ["latin"],
});

const geistMono = Geist_Mono({
  variable: "--font-geist-mono",
  subsets: ["latin"],
});

export const metadata: Metadata = {
  title: "DentIQ - AI Powered Dental Assistant",
  description: "Get instant dental advice through voice calls with our AI assistant. Available 24/7.",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <TanStackProvider>
      <ClerkProvider appearance={{
        variables: {
          colorPrimary: "#a48fff",
          colorBackground: "#f3f4f6",
          colorText: "#111827",
          colorTextSecondary: "#6b7280",
          colorInputBackground: "#f3f4f6"
        }
      }}>
        <html lang="en">
          <body className={`${geistSans.variable} ${geistMono.variable} antialiased dark`}>
            <UserSync />
            {children}
          </body>
        </html>
      </ClerkProvider>
    </TanStackProvider>
  );
}
```

### 5.3 Create User Sync Component

Create [src/components/UserSync.tsx](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/components/UserSync.tsx:0:0-0:0):

```typescript
"use client";
import { syncUser } from '@/lib/actions/users';
import { useUser } from '@clerk/nextjs';
import React, { useEffect } from 'react';

function UserSync() {
  const { isSignedIn, isLoaded } = useUser();

  useEffect(() => {
    const handleUserSync = async () => {
      if (isLoaded && isSignedIn) {
        try {
          await syncUser();
        } catch (error) {
          console.log("Failed to sync user", error);
        }
      }
    };
    handleUserSync();
  }, [isLoaded, isSignedIn]);

  return null;
}

export default UserSync;
```

### 5.4 Create User Sync Server Action

Create [src/lib/actions/users.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/lib/actions/users.ts:0:0-0:0):

```typescript
"use server";

import { currentUser } from "@clerk/nextjs/server";
import { prisma } from "../prisma";

export async function syncUser() {
  try {
    const user = await currentUser();
    if (!user) return;

    const existingUser = await prisma.user.findUnique({ where: { clerkId: user.id } });
    if (existingUser) return existingUser;

    const dbUser = await prisma.user.create({
      data: {
        clerkId: user.id,
        firstName: user.firstName,
        lastName: user.lastName,
        email: user.emailAddresses[0].emailAddress,
        phone: user.phoneNumbers[0]?.phoneNumber
      }
    });

    return dbUser;

  } catch (error) {
    console.log("Error in syncUser server action", error);
  }
}
```

---

## Step 6: Utility Functions Setup

### 6.1 Create Utility Functions

Create [src/lib/utils.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/lib/utils.ts:0:0-0:0):

```typescript
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}

export function generateAvatar(name: string, gender: "MALE" | "FEMALE") {
  const genderParam = gender === "MALE" ? "boy" : "girl";
  return `https://avatar.iran.liara.run/public/${genderParam}?username=${encodeURIComponent(name)}`;
}
```

### 6.2 Create Resend Client

Create [src/lib/resend.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/lib/resend.ts:0:0-0:0):

```typescript
import { Resend } from "resend";

const resend = new Resend(process.env.RESEND_API_KEY);

export default resend;
```

### 6.3 Create Vapi Client

Create [src/lib/vapi.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/lib/vapi.ts:0:0-0:0):

```typescript
import Vapi from "@vapi-ai/web";

export const vapi = new Vapi(process.env.NEXT_PUBLIC_VAPI_API_KEY as string);
```

### 6.4 Create TanStack Query Provider

Create `src/components/providers/TanStackProviders.tsx`:

```typescript
"use client";

import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { useState } from "react";

export default function TanStackProvider({ children }: { children: React.ReactNode }) {
  const [queryClient] = useState(() => new QueryClient());

  return (
    <QueryClientProvider client={queryClient}>
      {children}
    </QueryClientProvider>
  );
}
```

---

## Step 7: Server Actions Setup

### 7.1 Create Appointments Server Actions

Create [src/lib/actions/appointments.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/lib/actions/appointments.ts:0:0-0:0):

```typescript
"use server";

import { auth } from "@clerk/nextjs/server";
import { prisma } from "../prisma";
import { AppointmentStatus } from "@prisma/client";

function transformAppointment(appointment: any) {
  return {
    ...appointment,
    patientName: `${appointment.user.firstName || ""} ${appointment.user.lastName || ""}`.trim(),
    patientEmail: appointment.user.email,
    doctorName: appointment.doctor.name,
    doctorImageUrl: appointment.doctor.imageUrl || "",
    date: appointment.date.toISOString().split("T")[0],
  };
}

export async function getAppointments() {
  try {
    const appointments = await prisma.appointment.findMany({
      include: {
        user: {
          select: {
            firstName: true,
            lastName: true,
            email: true,
          },
        },
        doctor: { select: { name: true, imageUrl: true } },
      },
      orderBy: { createdAt: "desc" },
    });

    return appointments.map(transformAppointment);
  } catch (error) {
    console.log("Error fetching appointments:", error);
    throw new Error("Failed to fetch appointments");
  }
}

export async function getUserAppointments() {
  try {
    const { userId } = await auth();
    if (!userId) throw new Error("You must be logged in to view appointments");

    const user = await prisma.user.findUnique({ where: { clerkId: userId } });
    if (!user) throw new Error("User not found. Please ensure your account is properly set up.");

    const appointments = await prisma.appointment.findMany({
      where: { userId: user.id },
      include: {
        user: { select: { firstName: true, lastName: true, email: true } },
        doctor: { select: { name: true, imageUrl: true } },
      },
      orderBy: [{ date: "asc" }, { time: "asc" }],
    });

    return appointments.map(transformAppointment);
  } catch (error) {
    console.error("Error fetching user appointments:", error);
    throw new Error("Failed to fetch user appointments");
  }
}

export async function getUserAppointmentStats() {
  try {
    const { userId } = await auth();
    if (!userId) throw new Error("You must be authenticated");

    const user = await prisma.user.findUnique({ where: { clerkId: userId } });

    if (!user) throw new Error("User not found");

    const [totalCount, completedCount] = await Promise.all([
      prisma.appointment.count({
        where: { userId: user.id },
      }),
      prisma.appointment.count({
        where: {
          userId: user.id,
          status: "COMPLETED",
        },
      }),
    ]);

    return {
      totalAppointments: totalCount,
      completedAppointments: completedCount,
    };
  } catch (error) {
    console.error("Error fetching user appointment stats:", error);
    return { totalAppointments: 0, completedAppointments: 0 };
  }
}

export async function getBookedTimeSlots(doctorId: string, date: string) {
  try {
    const appointments = await prisma.appointment.findMany({
      where: {
        doctorId,
        date: new Date(date),
        status: {
          in: ["CONFIRMED", "COMPLETED"],
        },
      },
      select: { time: true },
    });

    return appointments.map((appointment) => appointment.time);
  } catch (error) {
    console.error("Error fetching booked time slots:", error);
    return [];
  }
}

interface BookAppointmentInput {
  doctorId: string;
  date: string;
  time: string;
  reason?: string;
}

export async function bookAppointment(input: BookAppointmentInput) {
  try {
    const { userId } = await auth();
    if (!userId) throw new Error("You must be logged in to book an appointment");

    if (!input.doctorId || !input.date || !input.time) {
      throw new Error("Doctor, date, and time are required");
    }

    const user = await prisma.user.findUnique({ where: { clerkId: userId } });
    if (!user) throw new Error("User not found. Please ensure your account is properly set up.");

    const appointment = await prisma.appointment.create({
      data: {
        userId: user.id,
        doctorId: input.doctorId,
        date: new Date(input.date),
        time: input.time,
        reason: input.reason || "General consultation",
        status: "CONFIRMED",
      },
      include: {
        user: {
          select: {
            firstName: true,
            lastName: true,
            email: true,
          },
        },
        doctor: { select: { name: true, imageUrl: true } },
      },
    });

    return transformAppointment(appointment);
  } catch (error) {
    console.error("Error booking appointment:", error);
    throw new Error("Failed to book appointment. Please try again later.");
  }
}

export async function updateAppointmentStatus(input: { id: string; status: AppointmentStatus }) {
  try {
    const appointment = await prisma.appointment.update({
      where: { id: input.id },
      data: { status: input.status },
    });

    return appointment;
  } catch (error) {
    console.error("Error updating appointment:", error);
    throw new Error("Failed to update appointment");
  }
}
```

### 7.2 Create Doctors Server Actions

Create [src/lib/actions/doctors.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/lib/actions/doctors.ts:0:0-0:0):

```typescript
"use server";

import { Gender } from "@prisma/client";
import { prisma } from "../prisma";
import { generateAvatar } from "../utils";
import { revalidatePath } from "next/cache";

export async function getDoctors() {
  try {
    const doctors = await prisma.doctor.findMany({
      include: {
        _count: { select: { appointments: true } },
      },
      orderBy: { createdAt: "desc" },
    });

    return doctors.map((doctor) => ({
      ...doctor,
      appointmentCount: doctor._count.appointments,
    }));
  } catch (error) {
    console.log("Error fetching doctors:", error);
    throw new Error("Failed to fetch doctors");
  }
}

interface CreateDoctorInput {
  name: string;
  email: string;
  phone: string;
  speciality: string;
  gender: Gender;
  isActive: boolean;
}

export async function createDoctor(input: CreateDoctorInput) {
  try {
    if (!input.name || !input.email) throw new Error("Name and email are required");

    const doctor = await prisma.doctor.create({
      data: {
        ...input,
        imageUrl: generateAvatar(input.name, input.gender),
      },
    });

    revalidatePath("/admin");

    return doctor;
  } catch (error: any) {
    console.error("Error creating doctor:", error);

    if (error?.code === "P2002") {
      throw new Error("A doctor with this email already exists");
    }

    throw new Error("Failed to create doctor");
  }
}

interface UpdateDoctorInput extends Partial<<CreateDoctorInput> {
  id: string;
}

export async function updateDoctor(input: UpdateDoctorInput) {
  try {
    if (!input.name || !input.email) throw new Error("Name and email are required");

    const currentDoctor = await prisma.doctor.findUnique({
      where: { id: input.id },
      select: { email: true },
    });

    if (!currentDoctor) throw new Error("Doctor not found");

    if (input.email !== currentDoctor.email) {
      const existingDoctor = await prisma.doctor.findUnique({
        where: { email: input.email },
      });

      if (existingDoctor) {
        throw new Error("A doctor with this email already exists");
      }
    }

    const doctor = await prisma.doctor.update({
      where: { id: input.id },
      data: {
        name: input.name,
        email: input.email,
        phone: input.phone,
        speciality: input.speciality,
        gender: input.gender,
        isActive: input.isActive,
      },
    });

    return doctor;
  } catch (error) {
    console.error("Error updating doctor:", error);
    throw new Error("Failed to update doctor");
  }
}

export async function getAvailableDoctors() {
  try {
    const doctors = await prisma.doctor.findMany({
      where: { isActive: true },
      include: {
        _count: {
          select: { appointments: true },
        },
      },
      orderBy: { name: "asc" },
    });

    return doctors.map((doctor) => ({
      ...doctor,
      appointmentCount: doctor._count.appointments,
    }));
  } catch (error) {
    console.error("Error fetching available doctors:", error);
    throw new Error("Failed to fetch available doctors");
  }
}
```

---

## Step 8: Update Package.json Scripts

Update your [package.json](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/package.json:0:0-0:0) scripts section:

```json
{
  "scripts": {
    "dev": "next dev --turbopack",
    "build": "prisma generate && next build --turbopack",
    "start": "next start",
    "lint": "biome check",
    "format": "biome format --write"
  }
}
```

---

## Step 9: Component Structure & Key Features

### Project Structure Overview

```
src/
├── app/
│   ├── admin/              # Admin dashboard for doctor management
│   ├── api/                # API routes (email sending)
│   ├── appointments/       # Appointment booking pages
│   ├── dashboard/          # User dashboard
│   ├── voice/              # AI voice assistant page
│   ├── layout.tsx          # Root layout with providers
│   └── page.tsx            # Landing page
├── components/
│   ├── admin/              # Admin-specific components
│   ├── appointments/       # Appointment-related components
│   ├── dashboard/          # Dashboard components
│   ├── emails/             # Email templates
│   ├── landing/            # Landing page components
│   ├── navbar.tsx          # Navigation bar
│   ├── providers/          # React providers
│   ├── ui/                 # shadcn/ui components
│   ├── voice/              # Voice assistant components
│   └── UserSync.tsx        # User sync component
├── hooks/                  # Custom React hooks
├── lib/
│   ├── actions/            # Server actions
│   ├── prisma.ts           # Prisma client
│   ├── resend.ts           # Resend client
│   ├── utils.ts            # Utility functions
│   ├── vapi-prompt.ts      # AI assistant prompt
│   └── vapi.ts             # Vapi client
└── middleware.ts           # Clerk middleware
```

### Key Pages to Create

#### 9.1 Landing Page ([src/app/page.tsx](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/app/page.tsx:0:0-0:0))

```typescript
import Hero from "@/components/landing/Hero";
import Header from "@/components/landing/Header";
import WhatToAsk from "@/components/landing/WhatToAsk";
import HowItWorks from "@/components/landing/HowItWorks";
import PricingSection from "@/components/landing/PricingSection";
import CTA from "@/components/landing/CTA";
import Footer from "@/components/landing/Footer";
import { currentUser } from "@clerk/nextjs/server";
import { redirect } from "next/navigation";

export default async function Home() {
  const user = await currentUser();
  if (user) redirect("/dashboard");
  
  return (
    <div className="min-h-screen bg-background">
      <Header />
      <Hero />
      <HowItWorks />
      <WhatToAsk />
      <PricingSection />
      <CTA />
      <Footer />
    </div>
  );
}
```

#### 9.2 Dashboard Page ([src/app/dashboard/page.tsx](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/app/dashboard/page.tsx:0:0-0:0))

```typescript
import ActivityOverview from "@/components/dashboard/ActivityOverview";
import MainActions from "@/components/dashboard/MainActions";
import WelcomeSection from "@/components/dashboard/WelcomeSection";
import Navbar from "@/components/navbar";

function DashboardPage() {
  return (
    <>
      <Navbar />
      <div className="max-w-7xl mx-auto px-6 py-8 pt-24">
        <WelcomeSection />
        <MainActions />
        <ActivityOverview />
      </div>
    </>
  );
}
export default DashboardPage;
```

#### 9.3 Voice Assistant Page ([src/app/voice/page.tsx](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/app/voice/page.tsx:0:0-0:0))

```typescript
import Navbar from "@/components/navbar";
import FeatureCards from "@/components/voice/FeatureCards";
import ProPlanRequired from "@/components/voice/ProPlanRequired";
import VapiWidget from "@/components/voice/VapiWidget";
import WelcomeSection from "@/components/voice/WelcomeSection";
import { auth } from "@clerk/nextjs/server";

async function VoicePage() {
  const { has } = await auth();
  const hasProPlan = has({ plan: "ai_basic" }) || has({ plan: "ai_pro" });

  if (!hasProPlan) return <ProPlanRequired />;

  return (
    <div className="min-h-screen bg-background">
      <Navbar />
      <div className="max-w-7xl mx-auto px-6 py-8 pt-24">
        <WelcomeSection />
        <FeatureCards />
      </div>
      <VapiWidget />
    </div>
  );
}

export default VoicePage;
```

#### 9.4 Admin Dashboard ([src/app/admin/page.tsx](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/app/admin/page.tsx:0:0-0:0))

```typescript
import AdminDashboardClient from "./AdminDashboardClient";

export default function AdminPage() {
  return <AdminDashboardClient />;
}
```

---

## Step 10: API Routes

### Email Sending Route

Create [src/app/api/send-appointment-email/route.ts](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/app/api/send-appointment-email/route.ts:0:0-0:0):

```typescript
import AppointmentConfirmationEmail from "@/components/emails/AppointmentConfirmationEmail";
import resend from "@/lib/resend";
import { NextResponse } from "next/server";

export async function POST(request: Request) {
  try {
    const body = await request.json();

    const {
      userEmail,
      doctorName,
      appointmentDate,
      appointmentTime,
      appointmentType,
      duration,
      price,
    } = body;

    if (!userEmail || !doctorName || !appointmentDate || !appointmentTime) {
      return NextResponse.json({ error: "Missing required fields" }, { status: 400 });
    }

    const { data, error } = await resend.emails.send({
      from: "DentIQ <no-reply@resend.dev>",
      to: [userEmail],
      subject: "Appointment Confirmation - DentIQ",
      react: AppointmentConfirmationEmail({
        doctorName,
        appointmentDate,
        appointmentTime,
        appointmentType,
        duration,
        price,
      }),
    });

    if (error) {
      console.error("Resend error:", error);
      return NextResponse.json({ error: "Failed to send email" }, { status: 500 });
    }

    return NextResponse.json(
      { message: "Email sent successfully", emailId: data?.id },
      { status: 200 }
    );
  } catch (error) {
    console.error("Email sending error:", error);
    return NextResponse.json({ error: "Internal server error" }, { status: 500 });
  }
}
```

---

## Step 11: Email Templates

Create `src/components/emails/AppointmentConfirmationEmail.tsx`:

```typescript
import {
  Body,
  Container,
  Head,
  Heading,
  Html,
  Link,
  Preview,
  Section,
  Text,
} from "@react-email/components";

interface AppointmentConfirmationEmailProps {
  doctorName: string;
  appointmentDate: string;
  appointmentTime: string;
  appointmentType?: string;
  duration?: number;
  price?: number;
}

export default function AppointmentConfirmationEmail({
  doctorName,
  appointmentDate,
  appointmentTime,
  appointmentType = "General Consultation",
  duration = 30,
  price = 0,
}: AppointmentConfirmationEmailProps) {
  return (
    <Html>
      <Head />
      <Preview>Your appointment has been confirmed</Preview>
      <Body style={main}>
        <Container style={container}>
          <Heading style={h1}>Appointment Confirmed</Heading>
          <Text style={text}>Hi there,</Text>
          <Text style={text}>
            Your appointment with <strong>{doctorName}</strong> has been successfully booked.
          </Text>
          <Section style={detailsContainer}>
            <Text style={detailText}>
              <strong>Date:</strong> {appointmentDate}
            </Text>
            <Text style={detailText}>
              <strong>Time:</strong> {appointmentTime}
            </Text>
            <Text style={detailText}>
              <strong>Type:</strong> {appointmentType}
            </Text>
            <Text style={detailText}>
              <strong>Duration:</strong> {duration} minutes
            </Text>
            {price > 0 && (
              <Text style={detailText}>
                <strong>Price:</strong> ${price}
              </Text>
            )}
          </Section>
          <Text style={text}>
            Please arrive 10 minutes before your appointment time.
          </Text>
          <Text style={text}>
            If you need to reschedule or cancel, please use our dashboard or contact us.
          </Text>
          <Link href={`${process.env.NEXT_PUBLIC_APP_URL}/dashboard`} style={button}>
            View Your Appointments
          </Link>
        </Container>
      </Body>
    </Html>
  );
}

const main = {
  backgroundColor: "#f6f9fc",
  fontFamily: "Arial, sans-serif",
};

const container = {
  backgroundColor: "#ffffff",
  margin: "0 auto",
  padding: "40px 20px",
  maxWidth: "600px",
};

const h1 = {
  color: "#333333",
  fontSize: "24px",
  fontWeight: "bold",
  marginBottom: "20px",
};

const text = {
  color: "#333333",
  fontSize: "16px",
  lineHeight: "24px",
  marginBottom: "16px",
};

const detailsContainer = {
  backgroundColor: "#f6f9fc",
  padding: "20px",
  borderRadius: "8px",
  margin: "20px 0",
};

const detailText = {
  color: "#333333",
  fontSize: "14px",
  marginBottom: "8px",
};

const button = {
  backgroundColor: "#a48fff",
  color: "#ffffff",
  padding: "12px 24px",
  borderRadius: "6px",
  textDecoration: "none",
  display: "inline-block",
  marginTop: "20px",
};
```

---

## Step 12: Running the Project

### 12.1 Install Dependencies

```bash
npm install
```

### 12.2 Generate Prisma Client

```bash
npx prisma generate
```

### 12.3 Push Database Schema

```bash
npx prisma db push
```

### 12.4 Seed Database (Optional)

Create a seed script to add sample doctors:

```bash
npx prisma db seed
```

### 12.5 Start Development Server

```bash
npm run dev
```

Visit `http://localhost:3000` to see your application.

---

## Step 13: Key Components to Build

### 13.1 Navbar Component ([src/components/navbar.tsx](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/components/navbar.tsx:0:0-0:0))

Create a navigation bar with:
- Logo
- Navigation links
- User menu (Clerk UserButton)
- Sign in/sign out buttons

### 13.2 Landing Page Components

Create these components in [src/components/landing/](cci:9://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/components/landing:0:0-0:0):
- `Header.tsx` - Navigation and logo
- `Hero.tsx` - Main hero section
- `HowItWorks.tsx` - How the service works
- `WhatToAsk.tsx` - What you can ask the AI
- `PricingSection.tsx` - Pricing plans
- `CTA.tsx` - Call to action
- `Footer.tsx` - Footer with links

### 13.3 Dashboard Components

Create these components in [src/components/dashboard/](cci:9://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/components/dashboard:0:0-0:0):
- `WelcomeSection.tsx` - Welcome message with user name
- `MainActions.tsx` - Quick action buttons (Book Appointment, Voice Assistant)
- `ActivityOverview.tsx` - Recent appointments and stats

### 13.4 Voice Components

Create these components in [src/components/voice/](cci:9://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/components/voice:0:0-0:0):
- `VapiWidget.tsx` - Voice assistant widget using Vapi
- `WelcomeSection.tsx` - Welcome message for voice page
- `FeatureCards.tsx` - Feature cards explaining capabilities
- `ProPlanRequired.tsx` - Upgrade prompt for free users

### 13.5 Admin Components

Create these components in [src/components/admin/](cci:9://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/components/admin:0:0-0:0):
- Doctor management table
- Add/Edit doctor forms
- Appointment overview

---

## Step 14: Styling Configuration

### 14.1 Update Tailwind Config

The project uses Tailwind CSS v4. Ensure your `tailwind.config.ts` is configured correctly.

### 14.2 Global Styles

Update [src/app/globals.css](cci:7://file:///Users/croma/Desktop/Desktop/Desktop%20-%20croma%E2%80%99s%20MacBook%20Air/Projects/dentiq/src/app/globals.css:0:0-0:0) with your theme variables and base styles.

---

## Step 15: Deployment

### 15.1 Vercel Deployment (Recommended)

1. Push your code to GitHub
2. Import project in Vercel
3. Add environment variables in Vercel dashboard
4. Deploy

### 15.2 Required Environment Variables in Production

```env
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
DATABASE_URL=
NEXT_PUBLIC_VAPI_API_KEY=
RESEND_API_KEY=
NEXT_PUBLIC_APP_URL=https://your-domain.com
```

---

## Summary of Key Features

1. **Authentication**: Clerk for user sign-up/sign-in
2. **Database**: PostgreSQL with Prisma ORM
3. **Appointment Booking**: Book appointments with doctors
4. **AI Voice Assistant**: Vapi integration for dental advice
5. **Email Notifications**: Resend for appointment confirmations
6. **Admin Dashboard**: Manage doctors and view appointments
7. **User Dashboard**: View appointments, book new ones, access AI
8. **Responsive Design**: Mobile-friendly with shadcn/ui components

---

## Next Steps for You

1. **Set up all required accounts** (Clerk, Database, Vapi, Resend)
2. **Create the project** following the initialization steps
3. **Configure environment variables** with your actual API keys
4. **Build out the UI components** following the structure above
5. **Test the application** locally
6. **Deploy to Vercel** when ready

This guide provides the complete foundation. You can now build out the specific UI components based on your design preferences while following the established architecture.

I've created a comprehensive step-by-step guide to build the DentIQ project from scratch. The guide covers:

**Account Setup:**
- Clerk (authentication)
- PostgreSQL database (Supabase/Neon/Railway)
- Vapi AI (voice assistant)
- Resend (email service)

**Technical Setup:**
- Next.js 15 project initialization
- shadcn/ui components installation
- Prisma database schema and setup
- Clerk authentication integration
- Environment variables configuration

**Core Features:**
- User authentication and sync
- Appointment booking system
- Doctor management
- AI voice assistant integration
- Email notifications
- Admin dashboard

**Key Files Created:**
- Database schema with User, Doctor, Appointment models
- Server actions for appointments, doctors, and users
- API route for email sending
- Email templates for appointment confirmations
- Utility functions and client configurations

The guide provides all the code you need to get the foundation running. You'll need to build out the UI components (landing page, dashboard, voice widget, admin panel) following the component structure I outlined.

Would you like me to elaborate on any specific part, such as the landing page components, dashboard implementation, or the voice assistant integration?