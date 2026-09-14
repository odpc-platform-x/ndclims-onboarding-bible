<img src="https://cdn.odpcx.com/public/idp/odpcx-logo.webp" alt="ODPCx Logo" style="height: 100px;" /> <img src="https://www.ndclims.com/ndclims-logo.svg" alt="NDCLIMS Logo" style="height: 100px;" />

# NDCLIMS Onboarding Bible

คู่มือ onboarding แบบ interactive สำหรับระบบ NDCLIMS (Thai national disease-control LIMS) — สำนักงานป้องกันควบคุมโรคที่ 10

## 📘 คู่มือ

| เล่ม             | อ่านโดย                             | ลิงก์                                                                                                                                                            |
| ---------------- | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Onboarding Bible | เจ้าหน้าที่ / Lab Admin / ผู้บริหาร | [odpc-platform-x.github.io/ndclims-onboarding-bible](https://odpc-platform-x.github.io/ndclims-onboarding-bible)                                                 |
| IT Runbook       | IT / Super Admin                    | [odpc-platform-x.github.io/ndclims-onboarding-bible/ndclims-it-runbook.html](https://odpc-platform-x.github.io/ndclims-onboarding-bible/ndclims-it-runbook.html) |
| Slide Orentaion        |  เจ้าหน้าที่ / Lab Admin / ผู้บริหาร | [odpc-platform-x.github.io/ndclims-onboarding-bible/presentation-onboarding.html](https://odpc-platform-x.github.io/ndclims-onboarding-bible/presentation-onboarding.html) |

## 🔗 ระบบจริง

| Site          | URL                                                            |
| ------------- | -------------------------------------------------------------- |
| NDCLIMS       | [odpc-10.ndclims.com](http://odpc-10.ndclims.com/)             |
| Clinexa Stock | [odpc-10.clinexa-stock.com](http://odpc-10.clinexa-stock.com/) |

## 🛠 Tech Stack

<p>
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white">
  <img alt="Fastify" src="https://img.shields.io/badge/Fastify-000000?style=for-the-badge&logo=fastify&logoColor=white">
  <img alt="Next.js" src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white">
  <img alt="React" src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black">
</p>
<p>
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white">
  <img alt="Drizzle ORM" src="https://img.shields.io/badge/Drizzle_ORM-C5F74F?style=for-the-badge&logo=drizzle&logoColor=black">
  <img alt="Redis" src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white">
</p>
<p>
  <img alt="pnpm" src="https://img.shields.io/badge/pnpm-F69220?style=for-the-badge&logo=pnpm&logoColor=white">
  <img alt="Turborepo" src="https://img.shields.io/badge/Turborepo-EF4444?style=for-the-badge&logo=turborepo&logoColor=white">
</p>

Monorepo: `apps/backend` (Fastify) · `apps/web` (Next.js/React) · `apps/agent` (desktop agent) · `packages/{types,validators,db}` (Drizzle ORM) — PostgreSQL + Redis + MinIO/S3

## สำหรับผู้แก้ไขเอกสาร

อ่าน [`HANDOFF.md`](./HANDOFF.md) ก่อนแก้ไฟล์ `index.html` / `ndclims-it-runbook.html` /`presentation-onboarding.html` — มี source-of-truth mapping กลับไปที่โค้ด backend จริง
