<script>
  import { marked } from "marked";
  import Dompurify from "isomorphic-dompurify";

  /** @type {import("vscode-languageserver-types").Hover} */
  export let value;

  /**
   * @param {import("vscode-languageserver-types").MarkedString[]} markedStrings
   * @returns {string}
   */
  function extractMarkedStrings(markedStrings) {
    return markedStrings
      .map((s) =>
        typeof s === "string" ? s : `\`\`\`${s.language}\n${s.value}\n\`\`\``,
      )
      .join("\n");
  }

  /**
   *
   * @param {import("vscode-languageserver-types").Hover} hover
   */
  function extractContents(hover) {
    let plaintext, markdown;

    if ("kind" in hover.contents) {
      if (hover.contents.kind === "plaintext") {
        plaintext = hover.contents.value;
      } else {
        markdown = hover.contents.value;
      }
    } else if (Array.isArray(hover.contents)) {
      markdown = extractMarkedStrings(hover.contents);
    } else {
      markdown = extractMarkedStrings([hover.contents]);
    }

    return { plaintext, markdown };
  }

  $: ({ plaintext, markdown } = extractContents(value));
</script>

<div class="Hover">
  {#if plaintext}
    <pre>{plaintext}</pre>
  {/if}

  {#if markdown}
    {@html Dompurify.sanitize(marked(markdown))}
  {/if}
</div>
