# 利用の流れ

## **LMSから、LTI認証を利用してJupyterHubへログイン**  

MCJ-CloudHubは、LMSのLTI認証利用が前提となっています。  

- 現在対応済みのLMS:
    - Moodle 4.0以降

## **ログインしたユーザ用の[Jupyter Notebook](https://github.com/jupyter/notebook)環境がDockerコンテナで起動する**  

LMSで選択したコースにフォーカスした設定で環境が起動します。  
[DockerSpawner](https://jupyterhub-dockerspawner.readthedocs.io/en/latest/spawner-types.html#dockerspawner)もしくは[SwarmSpawner](https://jupyterhub-dockerspawner.readthedocs.io/en/latest/spawner-types.html#swarmspawner)を利用して、認証されたユーザ用の環境がDockerコンテナで起動します。  
nbgraderを利用する際に、受講するコースを選択する箇所がありますが、ここにはログイン時に選択していたコースのみが表示されます。  

## **[nbgrader](https://github.com/jupyter/nbgrader)を利用して課題ファイルのやり取り・採点を行う**  

詳細は、[nbgrader公式](https://nbgrader.readthedocs.io/en/stable/)をご覧ください。  
MCJ-Cloudhubでの差分を以下に記載します。  

### nbgrader機能差分

- quickstartが使用不可  
    quickstartによって作成されるディレクトリや設定ファイルは、MCJ-CloudHubで設定している共通の設定により参照されないようになっているため、使用できません。

- 日本標準時（JST）以外への対応  
    日本標準時（JST）で使用することを前提としているため、変更できません。
