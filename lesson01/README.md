
# Lesson 01

In this Lesson the wizeliner will learn about the principal commands of terraform:

- Providers
- Resources 
- Principal commands:
    * terraform plan
    * terraform apply
    * terraform destroy
    * terraform variables
    * terraform local variables
    * terraform outputs
- My first deploy in AWS
    <details>
        <summary>Solution</summary>
        <table>
            <tr>
                <td><strong>main.tf</strong></td>
            </tr>
            <tr>
                <td>
                        provider "aws" {
                            region = "us-east-1"
                        }

                        resource "aws_instance" "miServidor" {
                            ami = var.ubuntu_ami
                            instance_type = var.instance_type
                            vpc_security_group_ids = [ aws_security_group.mi_grupo_de_seguridad.id ]
                            user_data = <<-EOF
                                        #!/bin/bash
                                        echo "Hola Terraformers!" > index.html
                                        nohup busybox httpd -f -p ${var.server_port} & 
                                        EOF
                        }

                        resource "aws_security_group" "mi_grupo_de_seguridad" {
                            name = "primer-servidor-sg"

                            ingress {
                                cidr_blocks = ["0.0.0.0/0"]
                                description = "Acceso al puerto web"
                                from_port = var.server_port
                                to_port = var.server_port
                                protocol = "TCP"
                            }
                        }
                </td>
            </tr>
        </table>
    </details>
