# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Site vitrine de l'agence web de Patxi Sallaberry (INSA, Saint-Pée-sur-Nivelle, Pays Basque). Cible principale : PME locales basques (campings indépendants, artisans bâtiment, restaurants, professions libérales, gîtes) avec sites obsolètes ou absents.

Positionnement : ingénieur local voisin, pas agence parisienne. Différenciateurs = visite physique, prénom Patxi, INSA.

## Stack actuelle

Site statique pur : `index.html` + `style.css`. Aucun outil de build, aucun framework, aucune dépendance. Ouvrir directement dans un navigateur ou servir avec `python3 -m http.server`.

## Stack cible (projets clients)

Astro (SSG) ou Next.js + Tailwind CSS + TypeScript + Vercel/Cloudflare Pages.

Chaque projet client démarre par un fichier `camping.config.ts` (ou `[secteur].config.ts`) avant tout composant.

**Règle absolue pour les clients hébergement/camping :** jamais de moteur de réservation maison — uniquement des iframes PMS avec fallback lien direct si l'iframe est bloquée.

## Architecture CSS (site vitrine)

Toutes les valeurs de design sont centralisées dans `:root` dans `style.css` :

```css
--color-primary, --color-secondary, --color-dark, --color-mid,
--color-light, --color-text, --color-muted,
--radius, --shadow, --transition, --font
```

Modifier ces variables pour adapter le thème. Ne pas coder des couleurs en dur dans les règles.

## Offre commerciale de référence

- Création site : 1 500–2 000 €
- Maintenance : 80 €/mois (2 modifications incluses, 1h max/mois)
- Délai livraison : 21 jours ouvrés
- Break-even : 3 clients récurrents = 240 €/mois

## Ordre de génération des composants (projets clients Astro)

`[secteur].config.ts → types.ts → constants.ts → Navbar.tsx → Hero.tsx → [sections métier] → BookingCTA.tsx → Footer.tsx → index.astro`

Un composant = un prompt = un fichier. Ne pas regrouper plusieurs composants dans un même fichier généré.
