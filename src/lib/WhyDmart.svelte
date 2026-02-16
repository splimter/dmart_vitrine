<script lang="ts">
  import mermaid from "mermaid";
  import { onMount } from "svelte";

  function isDarkMode() {
    return document.documentElement.classList.contains("dark");
  }

  async function renderMermaid() {
    const theme = isDarkMode() ? "dark" : "neutral";
    mermaid.initialize({ startOnLoad: false, theme });
    document.querySelectorAll(".mermaid[data-original]").forEach((el) => {
      el.removeAttribute("data-processed");
      el.innerHTML = el.getAttribute("data-original")!;
    });
    await mermaid.run();
  }

  onMount(() => {
    document.querySelectorAll("pre.mermaid").forEach((el) => {
      el.setAttribute("data-original", el.innerHTML);
    });
    renderMermaid();

    const onThemeChange = () => renderMermaid();
    window.addEventListener("themechange", onThemeChange);
    return () => window.removeEventListener("themechange", onThemeChange);
  });
</script>

<div class="content">
  <h1>Why DMART?</h1>
  <p class="intro">
    Unlock the true value of your data. DMART transforms data from a liability
    into an asset.
  </p>

  <div class="feature-section">
    <h2>Data First Philosophy</h2>
    <p>Traditional systems trap data. DMART liberates it.</p>

    <div class="diagram-container">
      <pre class="mermaid">
graph TD
    subgraph Traditional["Traditional"]
        App1[App A] &lt;--&gt; DB1[(DB A)]
        App2[App B] &lt;--&gt; DB2[(DB B)]
    end

    subgraph DMART["DMART Model"]
        D_App1[Web] --&gt; API&#123;API&#125;
        D_App2[Mobile] --&gt; API
        API &lt;--&gt; Engine[Engine]
        Engine &lt;--&gt; Files[(Files)]
    end
      </pre>
    </div>

    <div class="grid-list">
      <div class="item">
        <strong>Ownership</strong>
        <span>Open, human-readable files. No lock-in.</span>
      </div>
      <div class="item">
        <strong>Accessibility</strong>
        <span>Unified API for any app.</span>
      </div>
      <div class="item">
        <strong>Resilience</strong>
        <span>Backup-ready, version-controlled.</span>
      </div>
    </div>
  </div>

  <div class="feature-section">
    <h2>Scalable Benefits</h2>
    <p>Adapts to your needs, from startup to enterprise.</p>

    <h3>Small Business</h3>
    <ul>
      <li><strong>All-in-One:</strong> CMS, CRM, Inventory.</li>
      <li><strong>Low Maintenance:</strong> Simple file structure.</li>
      <li><strong>Cost-Effective:</strong> Easy deployment.</li>
    </ul>

    <h3>Medium Business</h3>
    <ul>
      <li><strong>Automation:</strong> Workflows and ticketing.</li>
      <li><strong>Unified View:</strong> Single source of truth.</li>
      <li><strong>Security:</strong> RBAC and audit trails.</li>
    </ul>

    <h3>Big Business</h3>
    <ul>
      <li><strong>Prototyping:</strong> Rapid internal tools.</li>
      <li><strong>Federation:</strong> Connect multiple instances.</li>
      <li><strong>Future-Proof:</strong> Standard open formats.</li>
    </ul>
  </div>

  <div class="feature-section">
    <h2>Conclusion</h2>
    <p class="highlight">
      <strong>Stop managing databases. Start managing assets.</strong>
    </p>
  </div>
</div>

<style>
  .content {
    color: var(--text-main);
  }

  h1 {
    font-size: 2rem;
    margin-bottom: 1rem;
    color: var(--text-main);
    border-bottom: 1px solid var(--border-color);
    padding-bottom: 0.5rem;
    text-transform: uppercase;
  }

  .intro {
    font-size: 1.1rem;
    color: var(--text-secondary);
    margin-bottom: 2rem;
    font-family: var(--font-sans);
  }

  .feature-section {
    margin-bottom: 3rem;
    padding: 1.5rem;
    background: var(--bg-secondary);
    border: 1px solid var(--border-color);
  }

  h2 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    color: var(--text-main);
    text-transform: uppercase;
  }

  h3 {
    font-size: 1.2rem;
    margin-top: 1.5rem;
    margin-bottom: 0.5rem;
    color: var(--text-main);
    text-transform: uppercase;
    border-bottom: 1px dashed var(--border-color);
    display: inline-block;
  }

  p {
    margin-bottom: 1rem;
    line-height: 1.5;
  }

  ul {
    margin-bottom: 1rem;
    padding-left: 1.2rem;
    list-style-type: square;
  }

  li {
    margin-bottom: 0.5rem;
    color: var(--text-secondary);
  }

  strong {
    color: var(--text-main);
    font-weight: 700;
  }

  .grid-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-bottom: 1.5rem;
  }

  .item {
    background: var(--bg-color);
    padding: 1rem;
    border: 1px solid var(--border-color);
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
  }

  .item strong {
    color: var(--text-main);
    font-size: 1rem;
    text-transform: uppercase;
  }

  .item span {
    font-size: 0.9rem;
    color: var(--text-secondary);
  }

  .diagram-container {
    background: var(--bg-color);
    padding: 1rem;
    border: 1px solid var(--border-color);
    margin: 1.5rem 0;
    overflow-x: auto;
  }

  pre.mermaid {
    background: transparent;
    padding: 0;
    margin: 0;
    font-family: monospace;
    border: none;
  }

  .highlight {
    font-size: 1.1rem;
    color: var(--text-main);
    text-align: center;
    margin-top: 1rem;
    padding: 0.8rem;
    background: var(--bg-color);
    border: 1px dashed var(--text-main);
    text-transform: uppercase;
  }
</style>
