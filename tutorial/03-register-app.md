<!-- markdownlint-disable MD002 MD041 -->

この手順では、Azure Active Directory 管理センターを使用して、新しい Azure AD ネイティブアプリケーションを作成します。

1. ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)へ移動して、**個人用アカウント** (別名: Microsoft アカウント)、または**職場/学校アカウント**を使用してログインします。

1. 左側のナビゲーションで **[Azure Active Directory]** を選択し、それから **[管理]** で **[アプリの登録]** を選択します。

    ![アプリの登録のスクリーンショット ](./images/aad-portal-app-registrations.png)

1. **[新規登録]** を選択します。 **[アプリケーションを登録]** ページで、次のように値を設定します。

    - `UWP Graph Tutorial` に **[名前]** を設定します。
    - **[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。
    - [**リダイレクト URI**] で、ドロップダウンを [**パブリッククライアント (モバイル & デスクトップ)**] に変更し`https://login.microsoftonline.com/common/oauth2/nativeclient`、値をに設定します。

    ![[アプリケーションを登録する] ページのスクリーンショット](./images/aad-register-app.png)

1. **[登録]** を選択します。 **UWP グラフのチュートリアル**ページで、**アプリケーション (クライアント) ID**の値をコピーして保存します。次の手順で必要になります。

    ![新しいアプリ登録のアプリケーション ID のスクリーンショット](./images/aad-application-id.png)
