[nomina.py](https://github.com/user-attachments/files/28896591/nomina.py)
# ============================================================
#   NOMINUS-OBREROS — Capa de Lógica de Negocio
#   Archivo: nomina.py
# ============================================================

import tkinter.messagebox as mb

def calcular_nomina(sueldo_base, bono_extra=0.0):
    """
    Recibe el sueldo base y un bono opcional.
    Retorna un diccionario con los valores calculados de ley.
    """
    try:
        sueldo_base  = float(sueldo_base)
        bono_extra   = float(bono_extra)

        if sueldo_base <= 0:
            raise ValueError("El sueldo base debe ser mayor a cero.")

        # Cálculo de retenciones de ley
        sso          = sueldo_base * 0.04    # Seguro Social Obligatorio
        faov         = sueldo_base * 0.01    # Fondo de Ahorro Vivienda
        rpat         = sueldo_base * 0.005   # Régimen Prestacional
        total_ret    = sso + faov + rpat

        # Bono de alimentación (20% del sueldo base)
        bono_aliment = sueldo_base * 0.20
        total_bonos  = bono_aliment + bono_extra

        # Sueldo neto final
        sueldo_neto  = sueldo_base + total_bonos - total_ret

        return {
            "sueldo_base":   round(sueldo_base,  2),
            "bono_aliment":  round(bono_aliment, 2),
            "bono_extra":    round(bono_extra,   2),
            "total_bonos":   round(total_bonos,  2),
            "sso":           round(sso,           2),
            "faov":          round(faov,          2),
            "rpat":          round(rpat,          2),
            "total_ret":     round(total_ret,     2),
            "sueldo_neto":   round(sueldo_neto,  2),
        }

    except ValueError as e:
        mb.showerror("Error de Cálculo", f"Dato inválido:\n{e}")
        return None
