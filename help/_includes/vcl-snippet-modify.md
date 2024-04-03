---
source-git-commit: 2d902a3926c6bbc6a9dc8afcbd667eddeaf3be7e
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---
# Inclure le fichier pour modifier le fichier VCL personnalisé pour Fastly

## Modification du fragment de code VCL personnalisé

1. [Connexion](/help/get-started/onboarding.md#access-your-admin-panel) à l’administrateur.

1. Cliquez sur **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Système**.

1. Développer **Cache de page complète** > **Configuration rapide** > **Fragments de code VCL personnalisés**.

   ![Gestion des fragments de code VCL personnalisés](/help/assets/cdn/fastly-manage-snippets.png)

1. Dans le _Action_ , cliquez sur l’icône des paramètres en regard du fragment de code à modifier.

1. Une fois la page rechargée, cliquez sur **Chargement rapide de VCL** dans le _Configuration rapide_ .

1. Une fois le transfert terminé, actualisez le cache en fonction de la notification dans la partie supérieure de la page.

>[!WARNING]
>
>La variable _Fragments de code VCL personnalisés_ L’option de l’interface utilisateur affiche uniquement les fragments de code ajoutés par le biais de l’administrateur Adobe Commerce. Si vous ajoutez des fragments de code à l’aide de l’API Fastly, utilisez l’API pour [gérer les](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
