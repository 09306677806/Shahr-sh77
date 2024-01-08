| アクション                          | 説明                                                                                                                                                                                                                                                                                  |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `remove_self_hosted_runner`    | セルフホストランナーが削除されたときにトリガーされます。                                                                                                                                                                                                                                                        |
| `register_self_hosted_runner`  | 新しいセルフホストランナーが登録されたときにトリガーされます。 詳しい情報については「[セルフホストランナーの追加](/actions/hosting-your-own-runners/adding-self-hosted-runners)」を参照してください。                                                                                                                                                 |
| `runner_group_created`         | セルフホストランナーグループが作成されたときにトリガーされます。 詳しい情報については「[セルフホストランナーグループについて](/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups#about-self-hosted-runner-groups)」を参照してください。                                                                                  |
| `runner_group_created`         | セルフホストランナーグループが削除されたときにトリガーされます。 詳しい情報については「[セルフホストランナーグループの削除](/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups#removing-a-self-hosted-runner-group)」を参照してください。                                                                               |
| `runner_group_runner_removed`  | セルフホストランナーをグループから削除するのにREST APIが使われたときにトリガーされます。                                                                                                                                                                                                                                    |
| `runner_group_runners_added`   | セルフホストランナーがグループに追加されたときにトリガーされます。 詳しい情報については、「[セルフホストランナーをグループに移動する](/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups#moving-a-self-hosted-runner-to-a-group)」を参照してください。                                                                       |
| `runner_group_runners_updated` | ランナーグループのメンバーリストが更新されたときにトリガーされます。 詳しい情報については「[Organizationのグループ内にセルフホストランナーをセットする](/rest/reference/actions#set-self-hosted-runners-in-a-group-for-an-organization)」を参照してください。                                                                                                      |
| `runner_group_updated`         | セルフホストランナーグループの設定が変更されたときにトリガーされます。 詳しい情報については「[セルフホストランナーグループのアクセスポリシーの変更](/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups#changing-the-access-policy-of-a-self-hosted-runner-group)」を参照してください。                                              |
| `self_hosted_runner_updated`   | ランナーアプリケーションが更新されたときにトリガーされます。 REST API及びUIを使って見ることができます。JSON/CSVエクスポートで見ることはできません。 詳しい情報については、「[セルフホストランナーについて](/actions/hosting-your-own-runners/about-self-hosted-runners#about-self-hosted-runners)」を参照してください。{% ifversion fpt or ghec %}
| `self_hosted_runner_online`    | ランナーアプリケーションが開始されたときにトリガーされます。 REST APIを通じてのみ見ることができます。UIあるいはJSON/CSVエクスポートでは見ることができません。 詳しい情報については「[セルフホストランナーのステータスチェック](/actions/hosting-your-own-runners/monitoring-and-troubleshooting-self-hosted-runners#checking-the-status-of-a-self-hosted-runner)」を参照してください。             |
| `self_hosted_runner_offline`   | ランナーアプリケーションが停止されたときにトリガーされます。 REST APIを通じてのみ見ることができます。UIあるいはJSON/CSVエクスポートでは見ることができません。 詳しい情報については、「[セルフホストランナーのステータスチェック](/actions/hosting-your-own-runners/monitoring-and-troubleshooting-self-hosted-runners#checking-the-status-of-a-self-hosted-runner)」を参照してください。{% endif %}