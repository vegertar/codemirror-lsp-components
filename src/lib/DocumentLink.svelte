<script>
  /** @type {import("vscode-languageserver-types").DocumentLink} */
  export let value;
</script>

<div class="DocumentLink">
  <a href="${value.target}">Follow link</a>
  <span>{`${value.tooltip || "(ctrl + click)"}`}</span>
</div>
