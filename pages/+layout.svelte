<!-- Fichier pour changer le logo Evidence de la page @ -->

<script>
  import "@evidence-dev/tailwind/fonts.css";
  import "../app.css";
  import { EvidenceDefaultLayout } from "@evidence-dev/core-components";
  export let data;
</script>

<!-- Récupération du fichier .png situé dans le répertoire static du projet -->
<EvidenceDefaultLayout {data} logo="/logo.png">
  <slot slot="content" />
</EvidenceDefaultLayout>
