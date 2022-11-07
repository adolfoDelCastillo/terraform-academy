
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

                <br>resource "aws_instance" "miServidor" {</br>
                    ami = "ami-08c40ec9ead489470"
                    instance_type = "t2.micro"
                    vpc_security_group_ids = [ aws_security_group.mi_grupo_de_seguridad.id ]
                    user_data = <<-EOF
                                #!/bin/bash
                                echo "Hola Terraformers!" > index.html
                                nohup busybox httpd -f -p 8080 & 
                                EOF
                }

                resource "aws_security_group" "mi_grupo_de_seguridad" {
                    name = "primer-servidor-sg"

                    ingress {
                        cidr_blocks = ["0.0.0.0/0"]
                        description = "Acceso al puerto web"
                        from_port = 8080
                        to_port = 8080
                        protocol = "TCP"
                    }
            }
                </td>
            </tr>
        </table>
    </details>
