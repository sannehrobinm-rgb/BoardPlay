# 🎲 BoardPlay

> Découvrez, comparez et gérez vos jeux de société — avec recommandations IA, carte interactive et visualisation de données.

![Status](https://img.shields.io/badge/status-en%20développement-orange)
![Stack](https://img.shields.io/badge/stack-Next.js%20%7C%20TypeScript%20%7C%20Prisma-blue)

---

## 🎯 Concept

BoardPlay est une plateforme fullstack dédiée aux jeux de société. Elle permet de cataloguer sa collection, de découvrir de nouveaux jeux via un moteur de recommandation IA, de visualiser les données sur une carte (localisation des joueurs) et de suivre ses parties.

---

## ✨ Fonctionnalités

- 🃏 Catalogue de jeux avec filtres avancés
- 🤖 Recommandation intelligente par IA
- 🗺️ Carte interactive des joueurs (Leaflet)
- 📊 Visualisation des statistiques (Recharts)
- 🏆 Suivi des parties et scores
- 📱 Interface responsive et animée

---

## 🛠️ Stack technique

| Couche | Technologie |
|--------|-------------|
| Framework | Next.js 14 (App Router) |
| Langage | TypeScript |
| UI | React + Tailwind CSS + shadcn/ui |
| Animations | Framer Motion |
| Carte | Leaflet |
| Graphiques | Recharts |
| ORM | Prisma |
| Base de données | PostgreSQL (Neon) |
| IA | API LLM (Claude / OpenAI) |
| Déploiement | Vercel |

---

## 🚀 Installation

```bash
git clone https://github.com/TON_USERNAME/boardplay.git
cd boardplay

npm install

cp .env.example .env.local
# → renseigner DATABASE_URL + LLM_API_KEY

npx prisma db push

npm run dev
```

---

## 📁 Structure du projet

```
src/
├── app/
│   ├── api/
│   │   ├── board-games/
│   │   ├── matches/
│   │   └── ai/recommend/
│   └── page.tsx
├── components/
│   ├── ui/
│   ├── layout/
│   ├── map/        # Composants Leaflet
│   └── charts/     # Composants Recharts
├── lib/
│   └── db.ts
├── types/
└── hooks/
prisma/
└── schema.prisma
```

---

## 🗄️ Modèles de données

```prisma
model BoardGame {
  id          String   @id @default(cuid())
  name        String
  minPlayers  Int
  maxPlayers  Int
  duration    Int      # en minutes
  category    String[]
  rating      Float?
  matches     Match[]
}

model Match {
  id         String    @id @default(cuid())
  date       DateTime  @default(now())
  game       BoardGame @relation(fields: [gameId], references: [id])
  gameId     String
  players    String[]
  winner     String?
}
```

---

## 📡 API Routes

| Méthode | Route | Description |
|---------|-------|-------------|
| GET | `/api/board-games` | Liste des jeux |
| POST | `/api/board-games` | Ajouter un jeu |
| GET | `/api/matches` | Historique des parties |
| POST | `/api/ai/recommend` | Recommandation IA |

---

## 👤 Auteur

Développé par **[TON NOM]** — projet de formation développeur web fullstack.
