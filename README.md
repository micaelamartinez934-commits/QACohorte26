# QACohorte26
Qa Automation 
README
Cypress QA Automation — Technology with Purpose by Santex
Repositorio de práctica para aprender QA Automation con Cypress, siguiendo el enfoque "Technology with Purpose" de Santex.

Contenido
Estructura básica de proyecto Cypress.
Ejemplos de tests e2e, tests de integración y pruebas de componentes (si aplica).
Configuración y scripts para ejecutar localmente.
Buenas prácticas y checklist de QA Automation aprendidas durante el curso.
Estructura recomendada
cypress/
fixtures/ — datos de prueba (JSON, imágenes, etc.)
integration/ — pruebas end-to-end
e2e/ — (alternativa moderna para e2e)
support/ — comandos personalizados y hooks
plugins/ — (si necesitas plugins de Cypress)
cypress.config.js — configuración principal de Cypress
package.json — scripts y dependencias
.gitignore
README.md — (este archivo)
docs/ — notas, checklist, recursos del curso
Requisitos
Node.js >= 16 (recomendado)
npm o yarn
Navegador compatible (Chrome, Edge, Firefox)
Instalación
Clonar el repositorio:


git clone <URL_DEL_REPO>
Instalar dependencias:


npm install
o


yarn
Scripts útiles (package.json)
"cypress:open" — abre la UI interactiva de Cypress:


npm run cypress:open
"cypress:run" — ejecuta tests en modo headless:


npm run cypress:run
"test" — alias para ejecutar una suite por defecto:


npm test
Ejemplo de package.json (fragmento):

json


{
  "scripts": {
    "cypress:open": "cypress open",
    "cypress:run": "cypress run",
    "test": "npm run cypress:run"
  },
  "devDependencies": {
    "cypress": "^12.0.0"
  }
}
Configuración recomendada (cypress.config.js)
Base URL para entornos de práctica.
Timeouts coherentes (commandTimeout, defaultCommandTimeout).
Video/screenshots activados para ejecuciones CI.
Ejemplo mínimo:
js


module.exports = {
  e2e: {
    baseUrl: 'http://localhost:3000',
    supportFile: 'cypress/support/e2e.js',
    setupNodeEvents(on, config) {
      // plugins
    }
  },
  video: true,
  screenshotsFolder: 'cypress/screenshots'
};
Convenciones y buenas prácticas
Organizar tests por feature, no por tipo de prueba.
Usar fixtures para datos repetidos.
Crear comandos personalizados en cypress/support/commands.js para acciones repetitivas (login, setup).
Mantener tests deterministas: evitar dependencias externas, limpiar estado entre pruebas.
Etiquetar tests con .only/.skip solo localmente, no subirlos al repo.
Revisar capturas y videos en CI cuando un test falla.
Usar Page Objects o Testing Library selectors para mayor mantenibilidad.
Ejemplo simple de test (cypress/e2e/login.cy.js)
js


describe('Login', () => {
  beforeEach(() => {
    cy.visit('/login');
  });

  it('permite iniciar sesión con credenciales válidas', () => {
    cy.get('[data-cy=email]').type('user@example.com');
    cy.get('[data-cy=password]').type('Password123');
    cy.get('[data-cy=submit]').click();
    cy.url().should('include', '/dashboard');
    cy.get('[data-cy=welcome]').should('contain', 'Bienvenido');
  });
});
Checklist de aprendizaje (Technology with Purpose — Santex)
Entender arquitectura de Cypress y ciclo de vida de los tests.
Configurar entornos de prueba locales y CI.
Crear y reutilizar fixtures y comandos.
Implementar pruebas e2e confiables y mantenibles.
Gestionar flakiness: retries, waits explícitos y limpieza de estado.
Integrar reportes (videos, screenshots, reporters como Mochawesome).
Automatizar ejecución en CI (GitHub Actions, GitLab CI, etc.).
Buen manejo de datos: creación/limpieza con APIs o DB seeds.
Integración con CI (ejemplo breve)
Configurar workflow en .github/workflows/ci.yml para:
Instalar dependencias
Iniciar servidor de la aplicación (o usar mock)
Ejecutar npm run cypress:run
Guardar artefactos (videos, screenshots, reportes)
Recursos y referencias
Documentación oficial de Cypress.
Guías y prácticas del curso "Technology with Purpose" de Santex.
Repositorios de ejemplo y plantillas de CI.
Cómo contribuir
Abrir issues para bugs o mejoras.
Enviar pull requests con pruebas claras y descripción del cambio.
Mantener branch limpio, tests pasando en CI.
Licencia
Indica la licencia del proyecto (por ejemplo MIT) o la política de Santex si aplica.

