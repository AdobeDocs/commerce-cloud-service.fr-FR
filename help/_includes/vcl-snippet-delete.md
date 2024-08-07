---
source-git-commit: 8f1ed3067f6daed897151052c8b9f987d3df3a50
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---
# Inclure le fichier pour supprimer le code VCL personnalisé pour Fastly

## Suppression du fragment de code VCL personnalisé

1. [Connectez-vous](/help/get-started/onboarding.md#access-your-admin-panel) à l’administrateur.

1. Cliquez sur **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Système**.

1. Développez **Cache de page complète** > **Configuration rapide** > **Fragments de code VCL personnalisés**.

   ![Gérer des fragments de code VCL personnalisés](/help/assets/cdn/fastly-manage-snippets.png)

1. Dans la colonne _Action_, cliquez sur l’icône de corbeille en regard de l’extrait de code à supprimer.

1. Dans la fenêtre modale suivante, cliquez sur **DELETE** et activez une nouvelle version.

>[!WARNING]
>
>L’option d’interface utilisateur _Fragments de code VCL personnalisés_ affiche uniquement les fragments de code ajoutés via l’administrateur Adobe Commerce. Si vous ajoutez des fragments de code à l’aide de l’API Fastly, utilisez l’API pour [les gérer](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-vcl-using-the-api).
