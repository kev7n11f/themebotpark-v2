```markdown
# Contributing to ThemeBotPark-v2

Welcome to ThemeBotPark! 🎢  
We're thrilled you're here to help build a universe of bots with flair, purpose, and immersion. Whether you're a developer, designer, storyteller, or dreamer—your contributions fuel the future of themed interaction.

---

## Guiding Principles

- **Modularity is Power**: Build small, scalable components that plug into any theme or bot persona.
- **Theme-First Thinking**: Every contribution should enhance the expressive richness of bot environments.
- **Creative Utility**: We value function _and_ form. Your code should be both elegant and purposeful.
- **Open Collaboration**: Respect different perspectives. Bots are characters, and we want a diverse cast.
- **Ethics Matter**: Be mindful with data usage, accessibility, and representation.

---

## How to Contribute

### 🔧 Code Contributions

1. **Fork the Repo** and create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Write Clean, Modular Code**  
   Follow our style guidelines (see below). Keep functionality isolated when possible.

3. **Test Thoroughly**  
   - Unit: `npm test`  
   - Integration: `npm run test:integration`  
   - Lint: `npm run lint`

4. **Pull Request Etiquette**  
   - Include a clear description  
   - Reference any related issues  
   - Add screenshots/logs if relevant  
   - Tag your PR with the appropriate labels (e.g., `enhancement`, `bugfix`, `theme-template`)

---

## 👩‍🎨 Creative Assets & Themes

Want to add a new bot persona or environment template?

- Use the CLI:  
  ```bash
  themebotpark scaffold theme <theme-id>
  themebotpark scaffold bot <bot-id>
  ```

- Place assets in:  
  ```
  themes/<theme-id>/assets/
  bots/<bot-id>/
  ```

- Update your config file and document your narrative/design choices in `README-theme.md`.

---

## 🤝 Contributor Code of Conduct

All contributors must follow our [Code of Conduct](./CODE_OF_CONDUCT.md).  
ThemeBotPark thrives on creativity and respect. Let's keep the park fun, safe, and inclusive for everyone.

---

## 🧭 Style Guide

- **Languages**: TypeScript, JSON5, YAML  
- **Format**: Use Prettier defaults  
- **Naming**: `kebab-case` for themes/bots, `camelCase` for variables  
- **Commits**: Use semantic prefixes (`feat:`, `fix:`, `chore:`)  

---

## 🗺️ Looking for Ideas?

Check out our [Roadmap](./README.md#roadmap) for open opportunities, or message us on GitHub Discussions.

---

## 🎁 Attribution & Licensing

All contributions must be licensed under the [MIT License](./LICENSE).  
If you use third-party assets, clearly document attribution and licensing in your theme's README.

---

Thanks for helping make ThemeBotPark a destination worth visiting again and again. 🛠️🌈
```

---

Feel free to drop this straight into the repo. If you want, I can also help write the `README-theme.md` template or even generate scaffolding for new themes based on your storytelling approach. Want to jam on the Noir Detective series next?
