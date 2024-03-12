---
title: 'wsl2 ってどうやってインストールするの？？'
emoji: '🐧'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['windows', 'wsl2', 'vscode']
published: true
published_at: 2023-09-16 15:10
---

# how to install `wsl2`

1. `windows の機能の有効化または無効化`

    1. `Linux 用 Windows サブシステムを有効化`

        ![Windows の機能のキャプチャ](/images/2023-09-16-how_to_install_wsl2/windows_function_menu.png)

1. install applications from `Microsoft Store`

    1. `ubuntu`

        ![ubuntu](/images/2023-09-16-how_to_install_wsl2/microsoft_store_ubuntu.png)

    1. `vscode`

        ![vscode](/images/2023-09-16-how_to_install_wsl2/microsoft_store_vscode.png)

1. `powershell` で実行

    1. `ubuntu` をディストリビューションとしてインストール

        ```wt
        wsl --install -d Ubuntu
        ```

        ![実行結果](/images/2023-09-16-how_to_install_wsl2/powershell_install_wsl.png)

    1. 文字化けエラーが出たのでアプデして対処

        ```wt
        wsl --update
        ```

        ![実行結果](/images/2023-09-16-how_to_install_wsl2/powershell_update_wsl.png)

    1. 任意のユーザー名・パスワードを設定

        ![実行結果](/images/2023-09-16-how_to_install_wsl2/powershell_create_username_password.png)

    1. `wsl` 内に入っていることを確認

        ```bash
        pwd
        ll
        ```

        ![実行結果](/images/2023-09-16-how_to_install_wsl2/powershell_wsl_confirm.png)

    1. `wsl` のバージョンが `2` であることを確認

        1. `wsl` から退出

            ```bash
            exit
            ```

        1. `powershell` で確認

            ```wt
            wsl -l -v
            ```

            ![実行結果](/images/2023-09-16-how_to_install_wsl2/powershell_wsl_exit.png)

1. `vscode` で開いてみる `F1` or `ctrl`+`shift`+`p` でコマンドパレットを開き、 `>wsl: Connect to WSL` より `wsl` を起動する

    ![wsl起動](/images/2023-09-16-how_to_install_wsl2/vscode_windows_connect_to_wsl.png)  
    ![実行結果](/images/2023-09-16-how_to_install_wsl2/vscode_wsl_loading.png)

1. `vscode` のターミナルを開く `ctrl`+`shift`+`` ` ``で新しいターミナルを開くと `wsl` のターミナル操作ができて幸せになれます。

    ![実行結果](/images/2023-09-16-how_to_install_wsl2/vscode_wsl_loaded.png)

## 参考

-   [以前のバージョンの WSL の手動インストール手順](https://learn.microsoft.com/ja-jp/windows/wsl/install-manual#step-1---enable-the-windows-subsystem-for-linux)
-   [WSL を使用して Windows に Linux をインストールする方法](https://learn.microsoft.com/ja-jp/windows/wsl/install#step-4---download-the-linux-kernel-update-package)
-   [WSL 開発環境を設定する](https://learn.microsoft.com/ja-jp/windows/wsl/setup/environment#set-up-your-linux-username-and-password)
