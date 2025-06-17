## 🔐 What is Azure NSG (Network Security Group)?

An **NSG (Network Security Group)** in Azure acts like a **firewall** that controls **network traffic** to and from Azure resources — like Virtual Machines (VMs), Subnets, etc.

It **decides**:

* What traffic is **allowed**
* What traffic should be **blocked**

It does this using a set of **rules** for both **inbound** (coming in) and **outbound** (going out) traffic.


## 🛡️ How Does an NSG Work?

### An NSG contains **security rules**. Each rule defines:

| Part            | What it means                                        |
| --------------- | ---------------------------------------------------- |
| **Name**        | The name of the rule                                 |
| **Priority**    | A number (100–4096) – lower number = higher priority |
| **Direction**   | Inbound (coming in) or Outbound (going out)          |
| **Port**        | Which port the rule applies to (like 22, 80)         |
| **Protocol**    | TCP, UDP, or Any                                     |
| **Source**      | Where the traffic is coming from                     |
| **Destination** | Where the traffic is going                           |
| **Action**      | Allow or Deny                                        |

---

## 🔧 Where Can You Apply NSGs?

You can apply NSGs to:

1. **Subnets** – Controls traffic for all VMs in that subnet.
2. **Network Interface (NIC)** – Controls traffic for a specific VM.

---

## 🧠 Simple Example:

Let’s say you have a Virtual Machine (VM) and you want to **only allow SSH (port 22)**:

1. **Allow Rule**:

   * Direction: Inbound
   * Port: 22
   * Action: Allow

2. **Deny All Rule**:

   * By default, Azure includes a rule that blocks all other traffic.

So only **SSH traffic** will be allowed, everything else will be blocked.

---

## 🔁 Is NSG Stateful?

Yes! NSGs are **stateful**, which means:

👉 If you allow incoming traffic (inbound), Azure automatically allows the response (outbound). You don’t have to create a separate outbound rule.

---

## 📝 Real-World Use Case Example:

Suppose your VM is a web server. You want:

| Purpose      | Rule                                   |
| ------------ | -------------------------------------- |
| Allow HTTP   | Inbound – Port 80 – Allow              |
| Allow HTTPS  | Inbound – Port 443 – Allow             |
| Allow SSH    | Inbound – Port 22 – Allow (for admins) |
| Block Others | Default Deny rule takes care of this   |

---

## ✅ Key Points to Remember:

* NSGs control **network access** to Azure resources.
* They are **stateful** – return traffic is automatically allowed.
* They can be applied at **subnet or NIC** level.
* Azure provides some **default rules**, and you can add **custom rules**.

---

