[English](README.md) | [Français](README.fr.md)

# Svelte + TS + Vite

Ce modèle vous aide à commencer un projet avec Svelte et TypeScript dans Vite.

## Configuration recommandée de l'IDE

[VS Code](https://code.visualstudio.com/) + [Svelte](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode).

## Besoin d'un framework Svelte officiel ?

Consultez [SvelteKit](https://github.com/sveltejs/kit#readme), qui utilise aussi Vite. Son approche serverless-first permet un déploiement sur différentes plateformes. Il prend directement en charge TypeScript, SCSS et Less. Vous pouvez facilement ajouter la prise en charge de mdsvex, GraphQL, PostCSS, Tailwind CSS et d'autres outils.

## Considérations techniques

**Pourquoi utiliser ce modèle plutôt que SvelteKit ?**

- SvelteKit fournit sa propre solution de routage, qui ne convient pas à tous les utilisateurs.
- SvelteKit est avant tout un framework qui utilise Vite en interne, et non une application Vite.
  Par exemple, `vite dev` et `vite build` ne fonctionnent pas dans un environnement SvelteKit.

Ce modèle contient le minimum nécessaire pour commencer avec Vite, TypeScript et Svelte. Il tient aussi compte de l'expérience de développement avec HMR et IntelliSense. Ses capacités sont comparables à celles des autres modèles `create-vite`. Il constitue un bon point de départ pour découvrir un projet Vite avec Svelte.

Si vous avez ensuite besoin des capacités et de l'extensibilité de SvelteKit, la structure similaire de ce modèle facilite la migration.

**Pourquoi utiliser `global.d.ts` plutôt que `compilerOptions.types` dans `jsconfig.json` ou `tsconfig.json` ?**

La définition de `compilerOptions.types` exclut tous les types qui ne figurent pas explicitement dans la configuration. Les références triple-slash conservent le comportement TypeScript par défaut, qui accepte les informations de type de tout l'espace de travail. Elles ajoutent aussi les informations de type de `svelte` et `vite/client`.

**Pourquoi inclure `.vscode/extensions.json` ?**

Les autres modèles recommandent indirectement des extensions dans leur README. Ce fichier permet à VS Code de proposer l'installation de l'extension recommandée à l'ouverture du projet.

**Pourquoi activer `allowJs` dans le modèle TS ?**

La valeur `allowJs: false` interdit les fichiers `.js` dans le projet. Elle n'interdit pas la syntaxe JavaScript dans les fichiers `.svelte`. Elle impose aussi `checkJs: false`. Le projet ne peut donc pas garantir que tout le code utilise TypeScript, et la vérification des types JavaScript existants devient moins précise. Un projet peut également avoir besoin d'une base de code mixte.

**Pourquoi HMR ne conserve-t-il pas l'état local de mon composant ?**

La conservation de l'état avec HMR présente plusieurs difficultés. Elle est désactivée par défaut dans `svelte-hmr` et `@sveltejs/vite-plugin-svelte`, car son comportement est souvent inattendu. Consultez les détails [ici](https://github.com/rixo/svelte-hmr#svelte-hmr).

Si un composant contient un état à conserver, créez un store externe que HMR ne remplacera pas.

```ts
// store.ts
// An extremely simple external store
import { writable } from 'svelte/store'
export default writable(0)
```
