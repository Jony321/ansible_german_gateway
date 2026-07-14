# ansible_german_gateway

Ansible-роль для автоматической настройки немецкого оптического аплинка (DE) и транзитного DHCP-сервера для виртуальных машин на физических гипервизорах Ubuntu 24.04.

## Требования

* ОС гипервизора: Ubuntu 24.04 LTS (Noble Numbat)
* Сетевой стек: Netplan + systemd-networkd
* Наличие установленной роли для управления фаерволом (рекомендуется `sorrowless.iptables`)

## Переменные роли (Defaults)

| Переменная | Значение по умолчанию | Описание |
|---|---|---|
| `german_interface` | `enp216s0f1` | Физический интерфейс немецкой оптики |
| `german_gateway` | `91.247.185.161` | Шлюз немецкого провайдера |
| `german_subnet` | `91.247.185.160/28` | Выделенная немецкая подсеть |
| `vm_private_subnet` | `10.99.0.0/24` | Серая транзитная сеть для ВМ |
| `vm_private_gateway` | `10.99.0.1` | Серый IP-шлюз на хосте |

*Переменная `german_ip` (уникальный белый IP хоста) задается индивидуально для каждого гипервизора в файле инвентаря.*

## Пример использования (Playbook)

```yaml
- name: Configure German Uplink on Hypervisors
  hosts: hypervisors
  become: true
  roles:
    - role: jony321.german_gateway
