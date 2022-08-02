# karabiner-config-raycast
左cmdダブルタップでraycastを起動したくて作った

## 貼り付ける
```
cat <<EOF > ~/.config/karabiner/assets/complex_modifications/144.json
{
  "title": "Raycast",
  "rules": [
    {
      "description": "Enter the left command key twice to bring up the Raycast window",
      "manipulators": [
        {
          "type": "basic",
          "from": {
            "key_code": "left_command",
            "modifiers": {
              "optional": ["any"]
            }
          },
          "to": [
            {
              "shell_command": "open /Applications/Raycast.app"
            }
          ],
          "conditions": [
            {
              "type": "variable_if",
              "name": "key pressed",
              "value": 1
            }
          ]
        },

        {
          "type": "basic",
          "from": {
            "key_code": "left_command",
            "modifiers": {
              "optional": ["any"]
            }
          },
          "to": [
            {
              "set_variable": {
                "name": "key pressed",
                "value": 1
              }
            },
            {
              "key_code": "left_command"
            }
          ],
          "description": "to_delayed_action is set to 400ms in karabiner.json",
          "to_delayed_action": {
            "to_if_invoked": [
              {
                "set_variable": {
                  "name": "key pressed",
                  "value": 0
                }
              }
            ],
            "to_if_canceled": [
              {
                "set_variable": {
                  "name": "key pressed",
                  "value": 0
                }
              }
            ]
          }
        }
      ]
    }
  ]
}
EOF
```
