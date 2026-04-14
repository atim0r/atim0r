<h1 align="center">
  Kari Atílio Moreira 
</h1>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Press+Start+2P&size=14&duration=3000&pause=1000&color=7EC850&center=true&vCenter=true&width=500&lines=%F0%9F%8C%BE+Fullstack+Developer;%E2%98%81%EF%B8%8F+Cloud+Explorer;%F0%9F%94%AD+Stargazer;%E2%9B%8F%EF%B8%8F+criador+do+OpenXNAX" alt="Typing SVG" />
</p>

<p align="center">
  <a href="https://github.com/karimoreira?tab=repositories"><img src="https://img.shields.io/badge/📦_Repos-62-7ec850?style=flat-square&labelColor=1c1710" alt="Repos"/></a>
  <a href="https://github.com/karimoreira?tab=followers"><img src="https://img.shields.io/badge/🌾_Followers-70-f0c040?style=flat-square&labelColor=1c1710" alt="Followers"/></a>
  <a href="https://github.com/karimoreira?tab=stars"><img src="https://img.shields.io/badge/⭐_Stars-11-e8822a?style=flat-square&labelColor=1c1710" alt="Stars"/></a>
  <a href="https://atiliodev.com"><img src="https://img.shields.io/badge/🏠_atiliodev.com-50a0e8?style=flat-square&labelColor=1c1710" alt="Portfolio"/></a>
  <a href="https://linkedin.com/in/atiliomoreira"><img src="https://img.shields.io/badge/💼_LinkedIn-50a0e8?style=flat-square&labelColor=1c1710" alt="LinkedIn"/></a>
</p>

---

<h2>🌌 Stardew Valley × Astropy</h2>

<p align="center">
  <img src="https://img.shields.io/badge/★_OBSERVATÓRIO_ESTELAR_★-Mapeando_commits_no_cosmos-1c1710?style=for-the-badge&labelColor=2a1c3d&color=7ec850" alt="Stardew Astropy Theme"/>
</p>

<table align="center">
  <tr>
    <td align="center" width="130">
      <a href="https://github.com/karimoreira?tab=repositories" style="text-decoration: none;">
        <b>🔭 Observação</b><br/>
        <sub>Astropy &<br/>Dados</sub>
      </a>
    </td>
    <td align="center" width="130">
      <a href="https://github.com/karimoreira?tab=repositories" style="text-decoration: none;">
        <b>⛏️ Mineração</b><br/>
        <sub>Backend &<br/>Databases</sub>
      </a>
    </td>
    <td align="center" width="130">
      <a href="https://github.com/karimoreira?tab=repositories" style="text-decoration: none;">
        <b>🌾 Cultivo</b><br/>
        <sub>Frontend &<br/>UI/UX</sub>
      </a>
    </td>
    <td align="center" width="130">
      <a href="https://github.com/karimoreira?tab=repositories" style="text-decoration: none;">
        <b>🌲 Coleta</b><br/>
        <sub>Cloud &<br/>DevOps</sub>
      </a>
    </td>
    <td align="center" width="130">
      <a href="https://github.com/karimoreira?tab=repositories" style="text-decoration: none;">
        <b>⚔️ Combate</b><br/>
        <sub>Testes &<br/>Debugs</sub>
      </a>
    </td>
  </tr>
</table>

<details>
<summary>🎒 <b>Abrir Telescópio / Inventário de Código</b> (clique para explorar)</summary>

<br/>
<p align="center">
  <i>"Assim como o cosmos obedece às leis da física, um bom software obedece ao Clean Code e ao SOLID." ☄️</i>
</p>

```python
from astropy.coordinates import SkyCoord
import astropy.units as u
from typing import Tuple

class FarmObservatory:
    """
    Monitoramento astronômico da fazenda Stardew.
    Desenvolvido com foco em SRP (Single Responsibility Principle) e encapsulamento seguro.
    """
    
    def __init__(self, farm_latitude: float, farm_longitude: float) -> None:
        # Encapsulamento estrito para proteger as coordenadas de alterações indevidas
        self.__farm_location = SkyCoord(
            ra=farm_latitude * u.degree, 
            dec=farm_longitude * u.degree, 
            frame='icrs'
        )
        self.__energy_level: int = 100

    def locate_iridium_meteorite(self, is_secure_environment: bool) -> Tuple[bool, str]:
        """
        Calcula a queda de um meteorito aplicando validações de segurança.
        """
        if not is_secure_environment:
            return False, "⚠️ Alerta de segurança: Ambiente não validado. Abortando observação."
            
        if self.__energy_level < 20:
            return False, "Energia baixa... vá dormir antes das 2h da manhã! 🛌"
            
        self.__energy_level -= 20
        ra_deg = round(self.__farm_location.ra.degree, 2)
        
        return True, f"☄️ Sucesso! Meteorito de Iridium detectado nas coordenadas RA {ra_deg}°."

# Instanciando e testando nosso código limpo sob as estrelas de Pelican Town 🌌
observatory = FarmObservatory(farm_latitude=45.5, farm_longitude=-122.6)
status, message = observatory.locate_iridium_meteorite(is_secure_environment=True)
